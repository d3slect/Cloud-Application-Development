title: Datastore Overview
content_class: smaller

- <https://developers.google.com/appengine/docs/python/datastore/overview>
- Distributed storage based on [Bigtable](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/cs//archive/bigtable-osdi06.pdf)
	- Highly scalable
	- In fact 6 Bigtables (1 for all the data, 4 for predefined indexes, 1 for user-defined indexes, [doc](https://developers.google.com/appengine/articles/storage_breakdown?hl=en#anc-tables))
- Replication across multiple data centers using the [Paxos algorithm](http://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/archive/paxos_made_live.pdf)
	- High availability (five 9s)
	- Eventual consistency ([wiki](http://en.wikipedia.org/wiki/Eventual_consistency))
- Entity = unit of data storage
	- kind, id, value, ...
- Entities located either directly via keys or in queries via pre-built indexes 
	- All queries are served via the indexes => limited but scalable queries 
	- Direct access via key can be simple/[batch](https://developers.google.com/appengine/docs/python/datastore/entities#Batch_Operations)/[async]()


---

title: Entities
content_class: smaller

- <https://developers.google.com/appengine/docs/python/datastore/entities>
- Identifier
	- User-supplied key name 
	- Automatically assigned numeric ID
- Named properties of various [types](https://developers.google.com/appengine/docs/python/datastore/entities#Properties_and_Value_Types)
	- Each can have one or more values 
- Kind: categorizes the entity for the purpose of queries
	- In python the Model class
- Model: prescription of an entity ([doc](https://developers.google.com/appengine/docs/python/datastore/datamodeling))
	- Individual entities of the same kind can have different sets of properties ([doc](https://developers.google.com/appengine/docs/python/datastore/datamodeling#The_Expando_Class))
	- Models can be hierarchic, allowing queries over a kind and its sub-kinds ([doc](https://developers.google.com/appengine/docs/python/datastore/datamodeling#The_PolyModel_Class))
- Key: enables direct access
	- Unique for each entity
	- Includes: entity's kind, identifier, ancestor path (later)
	- Permanent == cannot be changed

---

title: Entities II
subtitle: Ancestors
content_class: smaller

- Parent property
	- Entities form hierarchically structured space (similar to a file system)
	- Root entities: no parent
	- Permanent == cannot be changed
- Entity group
	- An entity and its descendants (transitive children)
	- Unit of transactionality (later)
- Ancestor path
	- Full path from the root entity to a given entity
	- Kind-identifier pairs
	- `Person:GreatGrandpa / Person:Grandpa / Person:Dad / Person:Me`

---

title: Queries
content_class: smaller

- <https://developers.google.com/appengine/docs/python/datastore/queries>
- Each query includes:
	- [Entity kind](https://developers.google.com/appengine/docs/python/datastore/entities#Kinds_and_Identifiers)
	- Zero or more [filters](https://developers.google.com/appengine/docs/python/datastore/queries#Filters) (based on property values, keys, ancestors)
		- Property queries may take one of the forms: =, <, <=, ..., !=, IN
	- Zero or more [sort orders](https://developers.google.com/appengine/docs/python/datastore/queries#Sort_Orders)

<pre class="prettyprint" data-lang="Python">
# Query interface constructs a query using instance methods
q = Person.all()
q.filter("last_name =", "Smith")
q.filter("height <=", max_height)
q.ancestor(ancestor_key)
q.order("-height")
</pre>

---

title: Queries II
content_class: smaller

- Queries are based solely on the indexes
  ([doc](https://developers.google.com/appengine/docs/python/datastore/queries#Restrictions_on_Queries))
	- First row of the corresponding index matching the filter is found (fast)
	- All the consecutive rows matching the filter are returned (up to the limit)
- Benefits
	- Scalable with the size of the result set
- Restrictions
	- A lot of indexes required
	- Entities lacking a property named in the query are ignored.
	- Filtering on unindexed properties returns no results.
	- Inequality filters are limited to at most one property, *but can include equality on another property:*

<pre class="prettyprint" data-lang="GQL">
SELECT * FROM Person WHERE last_name = :target_last_name
                       AND city = :target_city
                       AND birth_year >= :min_birth_year
                       AND birth_year <= :max_birth_year
</pre>


---

title: Queries III
content_class: smaller

- Restrictions cont.
	- Ordering of query results is undefined when no sort order is specified.
	- Sort orders are ignored on properties with equality filters.
	- Properties used in inequality filters must be sorted first.
	- Properties with multiple values can behave in surprising ways.
		- Depends on index search
		- At least one of the values satisfies *all* of the *inequality* filters
		- All of the *equality* filters are satisfied by *at least one* (each by potentially different) value
	- Queries inside transactions must include ancestor filters.
		- Entity group == unit of transactionality


---

title: Queries IV
content_class: smaller

- Retrieving data ([doc](https://developers.google.com/appengine/docs/python/datastore/queryclass#Query_run))
	- Limit on the number of results returned (to conserve resources)
	- Offset of the first returned entity
		- Still retrieved internally, better to use a [cursor](https://developers.google.com/appengine/docs/python/datastore/queries#Query_Cursors)
	- Internally retrieved in batches (batch size can be set)
	- Queries can have time-outs (maximum 60sec)
	
<pre class="prettyprint" data-lang="Python">
q = Person.all()
...

for p in q.run(offset=5, limit=5, batch_size=50, dealine=10):
  print "%s %s, %d inches tall" % (p.first_name, p.last_name, p.height)
</pre>

---

title: Special Types of Queries
content_class: smaller

- Projection Query ([doc](https://developers.google.com/appengine/docs/python/datastore/projectionqueries))
	- Retrieves only selected (indexed) properties
	- Runs solely on top of indexes (runs faster and costs less than normal query)
	- Entities returned by a projection query cannot be stored back
	- For multivalued properties generates all combination of found values (as stored in the index)
		- Including more than one multi-valued property in a projection requires an [exploding index](https://developers.google.com/appengine/docs/python/datastore/queries#Big_Entities_and_Exploding_Indexes)
- Keys-Only Query ([doc](https://developers.google.com/appengine/docs/python/datastore/queries#Keys_Only_Queries))
	- Returns only keys 
	- Usually combined with a batch read of the relevant entities
	- Same advantages/limitations as projection query 

---

title: Special Types of Queries II
content_class: smaller

- Kindles Query ([doc](https://developers.google.com/appengine/docs/python/datastore/queries#Kindless_Queries))
	- Cannot include filters or sort orders on property values
	- Can have filter on keys, `db.Query().filter('__key__ >', last_seen_key)`
	- Can have ancestor filter
- Ancestor query
	- Every query with an ancestor filter
	- `db.query_descendants()` to return a query for all descendants of a given entity

---

title: Cursors
content_class: smaller

- For fetching additional results of a query in a subsequent request without offset overhead
- String-encoded position in the index corresponding to the query
	- base64-encoded string, may expose the key (app ID, kind, key name or ID, and all ancestor keys) and properties used in the query (including filters and sort orders)
	- Cursor can be passed as HTTP GET/POST parameter or stored in datastore/memcache
- Can be used only by the same application to resume the same query
- A cursor determines an absolute position within an index
	- NOT a relative position in the result list
	- Data updates can have impact on the next results returned
- Both *start* and *end* cursors
	- You are not guaranteed that the size of the results will be the same as when you generated the cursors


---

title: Cursors II
content_class: smaller

<pre class="prettyprint" data-lang="Python">
people = Person.all()

person_cursor = memcache.get('person_cursor')
if person_cursor:
  people<b>.with_cursor(start_cursor=person_cursor)</b>

for person in people:
  # Do something

person_cursor = people<b>.cursor()</b>
memcache.set('person_cursor', person_cursor)
</pre>


---

title: Indexes
content_class: smaller

- <https://developers.google.com/appengine/docs/python/datastore/indexes>
- **Index** is a table containing entity keys of a given kind in a sequence specified by the index's properties
	- A column for every property in the index
	- A row for every entity in the Datastore that is a potential result for queries based on the index
	- Rows are sorted first by ancestor and then by property values, in the order specified in the index definition
- `index.yaml` configuration file ([doc](https://developers.google.com/appengine/docs/python/config/indexconfig))
	- Automatically updated by the dev. server when a new query is executed
- An entity is included in the index only if it has a value set for every property used in the index
	- Can have value `None`
- A *perfect index* ensures that all results for every possible execution of the query appear in consecutive rows of the index table


---

title: Indexes II
content_class: smaller

- A *perfect index* has (in the order of importance):
	- Properties used in equality filters
	- Property used in an inequality filter (of which there can be no more than one)
	- Properties used in sort orders
- During execution of a query, the Datastore:
	- Identifies the perfect index corresponding to the query
	- Scans from the beginning of the index to the first entity that meets all of the query's filter conditions
	- Continues scanning the index, returning each entity in turn, until it
		- encounters an entity that does not meet the filter conditions, or
		- reaches the end of the index, or
		- has collected the maximum number of results requested by the query.


---

title: Indexes III
content_class: smaller

- Indexes have [limits](https://developers.google.com/appengine/docs/python/datastore/overview#Quotas_and_Limits)
	- Maximum number of index entries for an entity (20000)
	- Maximum number of bytes in composite indexes for an entity (2 megabytes)
- [Exploding indexes](https://developers.google.com/appengine/docs/python/datastore/indexes#Index_Limits)
	- For entities with multiple properties where each has multiple values the index must include an entry *for every possible combination* of property values
	- The number of entries "explodes" combinatorially
	- For example the entity  
	<pre class="prettyprint" data-lang="Python">
		class Widget(db.Expando):
		  pass		
		e2 = Widget()
		e2.x = [1, 2, 3, 4]
		e2.y = ['red', 'green', 'blue']
		e2.date = datetime.datetime.now()
		e2.put()	
	</pre>	requires 12 index entries for the composite index `Widget(x, y, date)`


---

title: Indexes IV
content_class: smaller

- The number/type of indexes influences the cost of a single write ([doc](https://developers.google.com/appengine/docs/python/datastore/indexes#Index_Limits), [tutorial](https://developers.google.com/appengine/docs/python/datastore/entities#Understanding_Write_Costs))
	- 1 + the number of entries in the indexes the entity would appear in 
	- By default 3 indexes
		- `EntitiesByKind`
		- `EntitiesByProperty`
		- `EntitiesByPropertyDesc`
		- i.e., 1 for the kind index and then 2 for each property value. 
	- Exploding indexes slow down entity writes dramatically (and may cause the entity to exceed the index limit)
- Exploding indexes can be manually avoided ([tutorial](https://developers.google.com/appengine/articles/indexselection))




---

title: Data Consistency
content_class: smaller


- Two consistency levels ([doc](https://developers.google.com/appengine/docs/python/datastore/queries#Data_Consistency))
	- [Strong consistency](http://en.wikipedia.org/wiki/Strong_consistency): queries guarantee the freshest results, but may take longer to complete
	- [Eventual consistency](http://en.wikipedia.org/wiki/Eventual_consistency): queries generally run faster, but may occasionally return stale results
- Eventually consistent queries:
	- May use stale indexes
	- May sometimes return entities that no longer match the original query criteria
- Ancestor queries are strongly consistent by default
	- Can be made eventually consistent Datastore read policy
	- `Employee.all()...run(read_policy=db.EVENTUAL_CONSISTENCY)`
- Non-ancestor queries are always eventually consistent


---

title: Furthe Details on Datastore
content_class: smaller

- [https://developers.google.com/appengine/articles/datastore/overview]()

