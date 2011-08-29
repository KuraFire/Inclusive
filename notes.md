# Notes

This document is for notes related to the development and implementation of the Inclusive framework.

---

### Implementing Inclusive in an application

__Distribution__

* Build new application UI with Inclusive
* Making it easy to retrofit existing applications with Inclusive

__Grouping elements by skill__

* Identify which UI elements should be displayed by assigning a class? ("inclusive-1" through "inclusive-5")
    * What if we would offer a way for the dev to populate a map with tiny help bubbles that automatically 
      pop up next to newly-revealed UI elements? All you'd do as a dev is populate it with ID->helptext ?

__Sync to server__

* Developers need to be able to associate our calculated skill levels with their existing user objects
    * Do devs need to poll Inclusive then write to database?
    * Or do we trigger a callback after calculating levels?
    * ↳ We'll offer an API to retrieve a `userObject` that can be stored on the server, and simply overwritten 
      as an update. Similarly the server can push the `userObject` into Inclusive on the front-end if that one
      is out of date.

---

### Weighting individual metrics

__Positive impact__

* Use of customization features, a good indication that the user is comfortable hunting through preferences
* Use of keyboard shortcuts
* Use of advanced search techniques

__Negative impact__

* Consulting help or documentation, a good indication that the user is having difficulty using the application

__Ambiguous__

* Several metrics, particularly those involving time, may not be indicative of user skill (i.e. person could be multitasking)
    * Time between actions
    * Hover vs. click
    * Typing speed

The Ambiguous metrics can be used to reinforce either a positive or negative tilting. 

---
