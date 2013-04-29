
title: Agenda
content_class: smaller

- Other GAE Services
	- MapReduce & GAE MapReduce API
	- Google Big Query service
- Miscellaneous
	- Discussion on HWs.
	- Concluding remarks

---

title: Other GAE Services
subtitle: What else can be done with GAE	
class: segue dark nobackground

---

title: MapReduce 
content_class: smaller

- [wiki](http://en.wikipedia.org/wiki/MapReduce), [paper](http://research.google.com/archive/mapreduce.html)
- Computing model for processing of large data sets
- Distributed, parallel, scalable, ...
- General framework for implementing parallel processing
- Goal: Process as much data as possible, as fast as possible
- Used in a lot of Google (and other) products
- Idea:
	- Select and read in parallel the data to be processed 
	- Group the data, that should be processed together
	- Process the groups of the data belonging together in parallel

---

title: MapReduce Overview
content_class: smaller

<center>
![MapReduceOverview](images/mapreduce_mapshuffle.png)
</center>

---

title: MR Phase 1: Read
content_class: smaller

<img alt="Map" src="images/mr-read.png" style="float: right" />

- Reads data from storage and passes it to the next phase
- Can run in parallel
- Various forms of input data
	- GAE Datastore entities
	- Files on a file system
	- Entries from a zip archive
	- ...
- No user code 
	 

---

title: MR Phase 2: Map
content_class: smaller

<img alt="Map" src="images/mr-map.png"  style="float: right" />

- Filters and maps raw data input to a list of key-value pairs 
- Indicates which values should be processed together 
	- By assigning the same keys
- `Map(data) -> list(key, value)`
- User code
- Runs (in isolation) once per each piece of input data
	- Highly parallelizeable
- Can exploit data locality
	- Local data are passed to local mapper tasks
- Can be scaled
	- By increasing the number of parallel mapper tasks
- Usualy produces huge amounts of key-value pairs
	 

---

title: MR Phase 3: Shuffle
content_class: smaller

<img alt="Map" src="images/mr-shuffle.png"  style="float: right" />

- Groups the values that should be processed together
	- Based on the same keys of the key-value pairs 
- Complicated to parallelize
	- Includes sorting	
	- Huge sets of key-value pairs from map phase
- `Shuffle(list(key, value)) -> list(key, list(value))`
- No user code

---

title: MR Phase 4: Reduce
content_class: smaller

<img alt="Map" src="images/mr-reduce.png"  style="float: right" />

- Produces final output by processing corresponding values
	- Values of the key-value pairs with the same key are processed together
	- The lists of corresponding values might be pretty long
- `Reduce(key, list(value)) -> list(value)`
- User code
	- Usually includes most of the computation
- Runs (in isolation) once per each group of data with the same key
	- Easily parallelizeable
	- Different (coarser) granularity than map phase
 - Can be scaled
	- By increasing the number of parallel reduce tasks

---

title: MR Phase 5: Write
content_class: smaller

<img alt="Map" src="images/mr-write.png"  style="float: right" />

- Aggregates and stores the outputs produced in the reduce phase
- Has to serialized to some extent
- Various output formats
	- GAE Datastore entities
	- Files on a file system
	- ...
- No user code

---

title: MapReduce Summary
content_class: smaller

<center>
![MapReduceOverview](images/mapreduce_mapshuffle.png)
</center>

---

title: MapReduce on GAE
content_class: smaller

- [Google IO 2011 talk](http://www.google.com/events/io/2011/sessions/app-engine-mapreduce.html)

---

title: Further Reading
content_class: smaller

- [Google IO 2011](http://www.google.com/events/io/2011/sessions.html)
