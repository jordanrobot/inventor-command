### Inventor Command!

A command launcher for Autodesk Inventor.  Similar to Quicksilver, Launchy, Spotlight, Alfred, etc.

#### Description

Original idea is that this would be an add-in that will allow inventor users to quickly run ilogic rules from a launcher interface.  The user would hit a hotkey (perhaps ```!```) to invoke the launcher, presenting the user with a single text box.  As the user starts typing, a filtered list of ilogic rules is displayed below the text box.  The user may select an item from this list to activate it.  [See this image for reference.](https://hainproject.github.io/hain/images/demo.gif?width=400&height=263)

#### Planned Features

After some discussion on discord, several other uses were proposed.  A running list is presented below:

* Allow the activation of:

  * in-memory ilogic rules
  * current file ilogic rules?
  * vba macros (public subs w/out parameters)
  * inventor commands (ControlDefinitions)

* Possible manipulation/opening/right-click-menu of
  * Currently open documents
  * In-memory documents
  * referenced documents?
  * ability to restrict filtering by:
  * documents immediately referenced by currently open document
  * all documents referenced by currently open document 
  * all currently referenced documents (application-wide)
  * all open documents

* Other thoughts
  * Include fuzzy search?  (research options on this)
  * quicksilver has the concept of different "actions" that you can perform on a selection.  These actions may differ based on the selection (e.g. a file [open, show, copy, edit permissions, pipe, etc] will present different actions than an application [run, show, uninstall, etc]). 

#### Architecture thoughts

* Write in C# as an inventor add-in
* Develop an object for each type of launchable thing.
* Class: Launchable
  * Method: Activate
  * Property: Description
  * Property: others as needed
  * Property: Type
  * examples: LaunchableRule, LaunchableCommand, LaunchableDocument, LaunchableMacro

* Interface: Ilaunchable
  * Activate
  * Description
  * Type
  * ???
  
* Create indexers that knows how to build a list of each launchable type
  * Method: BuildLaunchabeIndex -> returns list of Ilaunchable, or <T>?
  
* Build a master searchable index (list of Ilaunchable) that we can filter.
  * When the master index is built, you can filter by Ilaunchable Types to include/remove various launchable types from the list when presenting to the user.  Use linq?
  * Set these by was of a configuration screen, or have another quicker way to access this?


#### Todo:

Look at how some of the other application launchers are structured for research.
