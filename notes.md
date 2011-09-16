# Notes

This document is for notes related to the development and implementation of the Inclusive framework.

---

### Launch thoughts

Faruk writes:

> Developing this will take a good amount of time, but I am already set to publish an article entitled *Inclusive Interface Design* relatively soon. I think it'll be best if we get a domain + one-page design made for it where we announce that this is now being developed, and people can sign up to our email newsletter for updates on when we'll go into beta etc.

> I just registered inclusiveframework.com and inclusiveui.com - any other obvious domain names we should get for this?

> I don't really like launchrock.com but it's a good inspiration of how simple this ought to be. Maybe add a field: "Describe in 140 characters or less what kind of app you're hoping to build with the Inclusive Framework" or something like that.

> We should also see which existing JavaScript app framework we can combine this with. Any preferences? Options (add any more you can think of):

* [SproutCore](http://www.sproutcore.com/)
* [Kendo](http://www.kendoui.com/)
* [Jo](http://joapp.com/)
* [Sencha](http://www.sencha.com/)
* [ActiveJS](http://www.activejs.org/)
* [Backbone.js](http://documentcloud.github.com/backbone/)
* [Cappuccino](http://cappuccino.org/)
* [Ender](http://ender.no.de/)

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

### Weighing individual metrics

__Positive impact__

* Use of customization features, a good indication that the user is comfortable hunting through preferences
* Use of keyboard shortcuts
* Use of advanced search techniques

__Negative impact__

* Consulting help or documentation, a good indication that the user is having difficulty using the application

__Ambiguous__

* We could try to count the number of times the browser's Back function is used, through URL hash changes or state object changes.
  If the user keeps jumping back and forth around the application, it could indicate trial and error.
* If the user's web browser happens to be identifiable as a cutting-edge development build, assume they have more technical prowess?
  This would obviously need to be taken lightly (the person could be using someone else's computer).
    * ↳ There's definitely some value to this, but it's getting increasingly less as Chrome is gaining mainstream market adoption.
* Several metrics, particularly those involving time, may not be indicative of user skill (i.e. person could be multitasking)
    * Time between actions
    * Hover vs. click
    * Typing speed
* For those metrics that measure elapsed time, we need to somehow account for extreme differences between recordings.
  If the user clicks around the interface within a short time period then stops for 5 minutes to do something else,
  the system cannot assume that the person is experiencing difficulties; they could be idling or focused elsewhere.
  We can determine an average reading and try to weed out values that seem unreasonable (by setting a certain acceptable threshold?)
    * Try to detect focus and blur, but this result cannot be relied upon.
    * ↳ This system should be able to identify spikes reliably and level them off to create more useful averages.

The Ambiguous metrics can be used to reinforce either a positive or negative tilting. 

---

### Random thoughts

Drag and drop -> if you drag an object from one place to the other, the interface doesn't know yet whether you want to move or copy it. Upon drop, this could pop up a menu of two items at your cursor position: “Move this object here” and “Add a copy of the object here”

These two menu items could each have a subtle shortcut key on the right of the item/clickable area, e.g.

	 Move object here                command
	 Add a copy of object here        option

That way, a pro user can recognize the keyboard shortcut identifiers and hold down each key once they figure it out. For non-pro users, the subtle thing on the right won't mean much and they'll ignore it, happily using the on-drop-menu instead.