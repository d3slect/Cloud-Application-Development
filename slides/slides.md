title: Agenda

[https://github.com/keznikl/Cloud-Application-Development]()

#Schedule

- **Lab 1** Intro, SDK, Hello World
- **Lab 2** Selection of features (datastore, tasks, blobs, ...)
- **Lab 3** Homework
	- preferably Python (easier to use)
	- individually or in small groups
- **Lab 4** Homework cont.
- **Lab 5** Summary and (maybe) map-reduce

#Requirements

- Google Account
- Python (basics of OOP, copy/paste) 


---

title: Introduction
subtitle: What is (not) Google App Engine
class: segue dark nobackground

---

title: What is Cloud Computing?
content_class: smaller

- Further reading
	- [Google Training Tutorial](https://developers.google.com/appengine/training/intro/whatiscc) 

---

title: What is Google App Engine?
content_class: smaller

<https://developers.google.com/appengine/>

- Platform for development of scalable cloud-based web apps
	- Motto: *Solutions that do not scale cannot be done at all!*
- PaaS - SDK for Python / Java / Go 
	- Runs on Google infrastructure
- Integrated with Google services
	- Management console and Google Accounts authentication
	- Can be integrated with Google Apps (own domain name, ...)
	- Access to API of Youtube and other Google services
- Free / paid option 
	- paid = pre-paid 'credit', works until depleted
- Further reading
	- [Google Training Tutorial](https://developers.google.com/appengine/training/intro/whatisgae)

---

title: What can App Engine do?
content_class: smaller

- Handle HTTP requests ([link](https://developers.google.com/appengine/docs/python/runtime#Requests))
- Store data
	- Focus on non-relational (entity-based) storage ([link](https://developers.google.com/appengine/docs/python/datastore/overview))
	- relational ([link](https://developers.google.com/cloud-sql/)) and blob ([link](https://developers.google.com/appengine/docs/python/blobstore/overview)) storage also available
- Process data asynchronously on background ([link](https://developers.google.com/appengine/docs/python/taskqueue/))
- Cache processed results for quick access ([link](https://developers.google.com/appengine/docs/python/memcache/))
- Render HTML from templates ([link](https://developers.google.com/appengine/docs/python/tools/webapp2))
- Push data to clients ([link](https://developers.google.com/appengine/docs/python/channel/))
- Download URL content ([link](https://developers.google.com/appengine/docs/python/urlfetch/))
- Send e-mails ([link](https://developers.google.com/appengine/docs/python/mail/))
- and much more... ([link](https://developers.google.com/appengine/docs/python/apis))

#It does everything in such a way that it scales!

---

title: Quotas
content_class: smaller

- [https://developers.google.com/appengine/docs/quotas]()
- Safety (daily, per minute), [billable](https://developers.google.com/appengine/docs/billing), fixed

<table>
  <tbody><tr>
    <th width="30%">Resource</th>
    <th>Free Default Daily Limit</th>
    <th>Billing Enabled Default Limit</th>
  </tr>
  <tr>
    <td>Blobstore Stored Data</td>
    <td>First 5 GB <br /><strong>Note:</strong> Not a daily limit but
a total limit.</td>
    <td>no maximum</td>
  </tr>
  <tr>
    <td>Code & Static Data Storage <br />(includes all versions)</td>
    <td>First 1 GB <br /><strong>Note:</strong> Not a daily limit but
a total limit.</td>
    <td>$0.13 per GB per month</td>
  </tr>
  <tr>
    <td>Stored Data <br />(billable)</td>
    <td>1 GB <br /><strong>Note:</strong> Not a daily limit but
a total limit.</td>
    <td>1 GB free; no maximum</td>
  </tr>
  <tr>
    <td>Number of Indexes</td>
    <td>200 <br /><strong>Note:</strong> Not a daily limit but
a total limit.</td>
    <td>200</td>
  </tr>
  <tr>
    <td>Read/Write Operations</td>
    <td>50,000</td>
    <td>Unlimited</td>
  </tr>
  <tr>
    <td>Outgoing Bandwidth <br />(billable, includes HTTPS)</td>
    <td>1 GB<br />56 MB/minute</td>
    <td>1 GB free; 14,400 GB maximum<br />10 GB/minute</td>
  </tr>
  <tr>
    <td>Incoming Bandwidth (includes HTTPS)</td>
    <td>1 GB; 14,400 GB maximum<br />56 MB/minute</td>
    <td>None</td>
  </tr>

</tbody></table>


---

title: Hello World
subtitle: Following the Google's Tutorial
class: segue dark nobackground

---

title: Dev Tools
content_class: smaller

#SDK 

- [Installation tutorial](https://developers.google.com/appengine/training/intro/gettingstarted#install)
- Python 2.7 ([link](http://www.python.org/getit/releases/2.7.3/)) 
- GAE Python SDK ([link](https://developers.google.com/appengine/downloads#Google_App_Engine_SDK_for_Python))
- Make sure that the python and GAE SDK directories added to PATH ([link](http://docs.python.org/2/using/windows.html#setting-envvars)).

#File types you will encounter

- Python sources (`.py`)
- YAML configuraiton files (`.yaml`)
- Web sources (`.html`, `.css`, ...)

#Recommended tools

- Your favorite text editor (vim, ...)
- IDLE: default Python editor ([link](http://docs.python.org/2/library/idle.html))
- Aptana Studio: Eclispe-based IDE ([link](http://www.aptana.com/))
- ...

---

title: Hello World
content_class: smaller

- [Getting started guide at GAE docs](https://developers.google.com/appengine/docs/python/gettingstartedpython27/helloworld)
- [Getting started tutorial at Google Training](https://developers.google.com/appengine/training/intro/gettingstarted)
<p></p>
- Create a skeleton of a new Google Appengine app
	- Choose an ID, e.g., `helloworld`
	- Use the *Google App Engine Launcher* ([tutorial](https://developers.google.com/appengine/training/intro/gettingstarted#creating))
- You should get the following structure ([tutorial](https://developers.google.com/appengine/training/intro/gettingstarted#hello))
	- `app.yaml` - configuration of the app
	- `main.py` - implementation of the req. handler
	- complete sources also available at [github](https://github.com/keznikl/Cloud-Application-Development/tree/master/hello-world)
- Test the app
	- Run the development server and visit <http://localhost:8080/>
	- Use the *Google App Engine Launcher* ([tutorial](https://developers.google.com/appengine/training/intro/gettingstarted#startdev)), or:

<pre class="prettyprint" data-lang="cmd">
python google_appengine/dev_appserver.py helloworld/
</pre>

---

title: App Configuration
content_class: smaller

The configuraiton of a GAE app is in the `app.yaml` file

<pre class="prettyprint" data-lang="YAML">
<b>application: helloworld
version: 1
runtime: python</b>27
api_version: 1
threadsafe: true

<b>handlers:
- url: /.*
  script: main.app</b>

...
</pre>

- Further reading
	- See the [official docs](https://developers.google.com/appengine/docs/python/config/appconfig) for further details on app configuration.


---

title: Handling Requests
content_class: smaller

Request handler is a specific Python object in a specific module referred in the `app.yaml` file; e.g., `app` in `main.py`

<pre class="prettyprint" data-lang="python">
import webapp2

class MainHandler(webapp2.<b>RequestHandler</b>):
    def <b>get</b>(self):
        self.<b>response.write</b>('Hello world!')

app = webapp2.WSGIApplication([('/', MainHandler)], debug=True)
</pre>

- Further reading
	- [webapp2 framework](https://developers.google.com/appengine/docs/python/tools/webapp2)

---

title: Uploading the App to Google
content_class: smaller

*"Feed the Big Brother"*

- Create the app in the GAE Administration Console ([link](https://appengine.google.com/))
	- Choose the same ID you've selected before
- Upload the app ([link](https://developers.google.com/appengine/docs/python/gettingstartedpython27/uploading), [link](https://developers.google.com/appengine/docs/python/tools/uploadinganapp))
	- You need to fill in your Google Account information
	- You can upload different versions for the same app ID and select which one is used as the default ([link](https://developers.google.com/appengine/docs/adminconsole/index))
	- Use the *Google App Engine Launcher* "Deploy" button ([tutorial](https://developers.google.com/appengine/training/intro/gettingstarted#upload)), or:
	
<pre class="prettyprint" data-lang="cmd">
python google_appengine/appcfg.py update helloworld/
</pre>

- Test the uploaded version
	- Default domain `http://your_app_id.appspot.com/`

---

title: Monitoring and Management 
content_class: smaller

- Development Console ([link](https://developers.google.com/appengine/docs/python/tools/devserver#The_Development_Console))
	- Basic infromation about the app in the *development* environment
	- Service usage/state overview (Datastore Viewer, Task Queues), Interactive Console 
	- SDK Console button in the *Google App Engine Launcher*
- Administrator Console ([link](https://developers.google.com/appengine/docs/adminconsole/?hl=en), [link](http://appengine.google.com))
	- All the 'possible' infromation about the app in the *production* environment
	- Service usage/state overview (again)
	- Resource usage, quotas (Main >> Quota Details)
	- Version management (Main >> Versions)
	- ...
- Try out and explore!


---

title: Guestbook app
subtitle: Following (again) the Google's Tutorial
class: segue dark nobackground

---

title: Guestbook App
content_class: smaller

<https://developers.google.com/appengine/docs/python/gettingstartedpython27/>

- Google Accounts for authentication ([tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/usingusers))
- Users post text messages via HTML forms ([tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/handlingforms))
- Datastore for storage of persistent data ([tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/usingdatastore))
- Jinja2 templating engine for HTML rendering ([tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/templates))

---

title: Using the Users Service
content_class: smaller

- [Tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/usingusers)
- Users API ([docs](https://developers.google.com/appengine/docs/python/users/))
	- Google authentication
	- Access to basic Google user properties (nickname, email)

<pre class="prettyprint" data-lang="python">
import webapp2
<b>from google.appengine.api import users</b>

class MainPage(webapp2.RequestHandler):
    def get(self):
        <b>user = users.get_current_user()</b>

        <b>if user:</b>
            self.response.headers['Content-Type'] = 'text/plain'
            self.response.out.write('Hello, ' + <b>user.nickname()</b>)
        <b>else:</b>
            self.redirect(<b>users.create_login_url(self.request.uri)</b>)

app = webapp2.WSGIApplication([('/', MainPage)], debug=True)
</pre>

---

title: Handling Forms
content_class: smaller

- [Tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/handlingforms), [webapp2 framework docs](http://webapp-improved.appspot.com/)

<pre class="prettyprint" data-lang="python">
<b>import webapp2</b>

class <b>MainPage</b>(webapp2.RequestHandler):
    <b>def get(self):</b>
        self.response.out.write("""
          &lt;html>
            &lt;body>
              &lt;form <b>action="/sign"</b> method="post">
                &lt;div>&lt;textarea name="content" rows="3" cols="60">&lt;/textarea>&lt;/div>
                &lt;div>&lt;input type="submit" value="Sign Guestbook">&lt;/div>
              &lt;/form>
            &lt;/body>
          &lt;/html>""")

class <b>Guestbook</b>(webapp2.RequestHandler):
    <b>def post(self):</b>
        self.response.out.write('&lt;html>&lt;body>You wrote:&lt;pre>')
        self.response.out.write(<b>self.request.get('content')</b>)
        self.response.out.write('&lt;/pre>&lt;/body>&lt;/html>')

app = webapp2.WSGIApplication([<b>('/', MainPage)</b>,
                              <b>('/sign', Guestbook)</b>],
                              debug=True)
</pre>

---

title: Using the Datastore
content_class: smaller

- [Tutorial](https://developers.google.com/appengine/docs/python/gettingstartedpython27/usingdatastore), [Datastore docs](https://developers.google.com/appengine/docs/python/datastore/)

#Modeling data

<pre class="prettyprint" data-lang="python">
from google.appengine.ext import db

class Greeting(db.Model):
    author = db.StringProperty()
    content = db.StringProperty(multiline=True)
    date = db.DateTimeProperty(auto_now_add=True)
</pre>

#Storing data

<pre class="prettyprint" data-lang="python">
class Guestbook(webapp2.RequestHandler):
    def post(self):
      guestbook_name = self.request.get('guestbook_name')
      <b>greeting = Greeting(parent=guestbook_key(guestbook_name))</b>

      if users.get_current_user():
        greeting.author = users.get_current_user().nickname()

      greeting.content = self.request.get('content')
      <b>greeting.put()</b>
      self.redirect('/?' + urllib.urlencode({'guestbook_name': guestbook_name}))
</pre>

---

title: Using the Datastore II.
content_class: smaller

#Retrieving data

- GQL ([docs](https://developers.google.com/appengine/docs/python/datastore/gqlreference))

<pre class="prettyprint" data-lang="python">
greetings = db.GqlQuery("SELECT * "
                        "FROM Greeting "
                        "WHERE ANCESTOR IS :1 "
                        "ORDER BY date DESC LIMIT 10",
                         guestbook_key(guestbook_name))

</pre>

<pre class="prettyprint" data-lang="python">

greetings = Greeting.gql("WHERE ANCESTOR IS :1 ORDER BY date DESC LIMIT 10",
                          guestbook_key(guestbook_name))
</pre>

- Query API ([docs](https://developers.google.com/appengine/docs/python/datastore/queries))

<pre class="prettyprint" data-lang="python">
greetings = Greeting.all()
greetings.ancestor(guestbook_key(guestbook_name))
greetings.filter("date >", datetime.datetime.now() + datetime.timedelta(days=-7))
greetings.order("-date")
</pre>

---

title: Slide Title
subtitle: Subtitle
class: image

![Mobile vs desktop users](image.png)

---

title: Slide Title
subtitle: Subtitle
class: image

![Mobile vs desktop users](image.png)

---

title: Segue Slide
subtitle: Subtitle
class: segue dark nobackground

---

title: Agenda
class: big
build_lists: true

Things we'll cover (list should build):

- Bullet1
- Bullet2
- Bullet3

---

title: Today
class: nobackground fill

![Many kinds of devices.](image.png)

<footer class="source">source: place source info here</footer>

---

title: Big Title Slide
class: title-slide

---

title: Code Example

Media Queries are sweet:

<pre class="prettyprint" data-lang="css">
@media screen and (max-width: 640px) {
  #sidebar { display: none; }
}
</pre>

---

title: Once more, with JavaScript

<pre class="prettyprint" data-lang="javascript">
function isSmall() {
  return window.matchMedia("(min-device-width: ???)").matches;
}

function hasTouch() {
  return Modernizr.touch;
}

function detectFormFactor() {
  var device = DESKTOP;
  if (hasTouch()) {
    device = isSmall() ? PHONE : TABLET;
  }
  return device;
}
</pre>

---

title: Centered content
content_class: flexbox vcenter

This content should be centered!
