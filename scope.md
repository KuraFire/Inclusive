# Scope outline

This document is for gathering details about the scope of Inclusive’s features and implementation.

---

### Metrics to track:

* Time between actions
* Time between sessions (for app use decay)
* Hovering vs. Clicks
* Frequency of keyboard shortcuts use
* Frequency of Help section use
* Frequency of Undo function use
* Typing speed
* Dialog dismiss behavior: Cancel vs. Action
* Use of customization features
* Button familiarities:
    * Escape
    * Home/End
* Use of advanced search techniques

---

### Storage and processing of metrics data

* Use window.localStorage
    * **REQUIRED**: built-in mechanism for syncing to server (so the information can be stored for the user account, not the browser)
* Weighting of metrics for algorithmic determination of the user skill level
    * Customization of weighting scales only for those diving into the raw source

---

### Development & Implementation

* Skill trees:
    * One default object with multiple, linear skill levels (e.g. Beginner, Intermediate, Advanced)
    * Grouping by feature-set or subject matter: multiple objects with (linear) skill levels in each, user gains experience across all groups (objects)
    * Skill levels are represented as a numerical index, customizable (default: 1–5)
    * Default skill group can be averaged aggregate of all sub-groups (if created)

* Events:
    * When a user gains a level, on a per-group granularity
    * When a user drops a level (usage decay -> offer the user a quick refresher of the UI, if so desired)
        * After level decay, all experience gains are accelerated (by e.g. 150% — should be customizable!)
    * Allow the developer to hook into our event gathering model to insert communication to the user where desired

* Polls / surveys:
    * Ability to ask the user for their approval / disapproval of UI changes upon gaining or losing a level
    * Helps us to determine if our algorithms are tuned properly (“is the user really ready for this change or are we too eager?”)
    * Helps the developer fine-tune their groups and skill level designations

* Developer polls `Inclusive.user.skills.level` (for example), or `Inclusive.user.skills.someGroup.level` to determine when to show UI elements and features

* Inline UI help indicators for communicating with the user; when a user gains a skill level, UI popups can be used to communicate new features or options to the user
    * See: Events section above; developer can hook into our event gathering model for inline UI help/communications