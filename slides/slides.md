title: Agenda
class: big

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

[Google Training Tutorial](https://developers.google.com/appengine/training/intro/whatiscc) 

---

title: What is (isn't) Google App Engine?

- [https://developers.google.com/appengine/]()
- [Google Training Tutorial](https://developers.google.com/appengine/training/intro/whatisgae)
- Platform for development of scalable cloud-based web apps
	- Motto: *Solutions that do not scale cannot be done at all!*
- PaaS - SDK for Python / Java / Go 
	- Runs on Google infrastructure
- Integrated with Google services
	- Management console and Google Accounts authentication
	- Can be integrated with Google Apps (domain name, ...)
	- Access to API of Youtube and other google services
- Free / paid option 
	- paid = pre-paid 'credit', works until depleted

---

title: What can App Engine do?


- Handle HTTP requests ([todo]())
- Store data
	- Focus on non-relational (entity-based) storage ([todo]())
	- relational ([todo]()) and blob ([todo]()) storage also available
- Process data asynchronously on background ([todo]())
- Cache processed results for quick access ([todo]())
- Render HTML from templates ([todo]())
- Push data to clients ([todo]())
- Download URL content ([todo]())
- Send e-mails ([todo]())
- and much more...

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
- Python 2.7 ([link](http://www.python.org/getit/releases/2.7/)) 
- GAE Python SDK ([link](https://developers.google.com/appengine/downloads))
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

- [Getting started guide on GAE docs](https://developers.google.com/appengine/docs/python/gettingstartedpython27/)
- [Getting started guide on Google Training](https://developers.google.com/appengine/training/intro/gettingstarted)

- Create a skeleton of a new Google Appengine app
	- Use the *Google App Engine Launcher* ([todo]())
- Implement the main request handler

<pre class="prettyprint" data-lang="python">
import webapp2

class MainPage(webapp2.<b>RequestHandler</b>):
  def <b>get</b>(self):
      self.response.headers['Content-Type'] = 'text/plain'
      self.<b>response.write</b>('Hello, webapp2 World!')

app = webapp2.WSGIApplication([('/', MainPage)], debug=True)
</pre>

- Run the development server:
	- Use the *Google App Engine Launcher* ([todo]()), or:

<pre class="prettyprint" data-lang="cmd">
python dev_appserver.py &lt;path_to_your_app&gt;
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
