title: Agenda
class: big
content_class: smaller

###Schedule

- **Lab 1** Intro, SDK, Hello World
- **Lab 2** Selection of features
	- datastore, tasks, blobs, ... 
- **Lab 3** Homework
	- preferably Python (easier to use)
	- individually or in small groups
- **Lab 4** Homework cont.
- **Lab 5** Summary and (maybe) map-reduce

###Requirements

- Google Account
- Python (basics of OOP, copy/paste) 

[https://github.com/keznikl/Cloud-Application-Development]()

---

title: Introduction
subtitle: What is (not) Google App Engine
class: segue dark nobackground

---

title: App Engine Introduction
content_class: smaller

- [https://developers.google.com/appengine/]()
- Platform for development of **scalable** cloud-based web apps
- PaaS - SDK for Python / Java / Go 
- Management console and Google Accounts authentication
- Can be integrated with Google Apps (domain name, gmail, ...)
- Free / paid option (paid = pre-paid 'credit', works until depleted)

---

title: Hello World
subtitle: Following Google's Tutorial
class: segue dark nobackground

---

title: Hello World
content_class: smaller

[Getting started guide](https://developers.google.com/appengine/docs/python/gettingstartedpython27/)

###SDK
Download and install:

- Python 2.7 ([http://www.python.org/getit/releases/2.7/]())
- GAE Python SDK ([https://developers.google.com/appengine/downloads]())


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
