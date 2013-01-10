What's new in v3 of the XPage Debug Toolbar

IMPORTANT: the dBar managed bean property "enabled" has been renamed to "toolbarVisible" and defaults to false. This is done so you can leave all dBar.someFunction() calls intact when moving an applicationn to production. If the toolbarVisible property remains false, the calls won't do anything (and thus have no negative impact on your application's performance). The toolbarVisible property works independant from any configured external logging database, so you can still have external logging of (for instance) only warnings and errors without showing the toolbar at all (or only showing it to users with the [debug] role). Normally you don't need to use this property: it is automatically set when the toolbar is rendered in a browser.

There's 1 downside to this: the toolbarVisible property is automatically set to true in the ccDebugToolbar's beforPageLoad event (since the toolbar is loaded) so any dBar.XXX calls in the calling XPages's beforePageLoad event won't have an effect. To change this behaviour, you can set the property as a managed property in the dBar bean configuration.

- Layout changes
	- simplified CSS (i.e. CSS3 selectors for zebra tables)
	- better compatibility with Bootstrap/ JQM
	
- Removed "Timers" tab
	- startTimer() en stopTimer() are now deprecated (replaced by debug() calls)
	
- New options in Messages tab: detailed timings
	- shows milliseconds for every log message
	
- New feature: read server log files

- Redesigned Inspector:
	- removed debug toolbar components from component selection list
	- executing a statement now does a full refresh, so you can instantly see the effect (try a btn.setDisabled(true) for instance!)
	- sortering component ids: alles wat begint met een _ achteraan
	- layout changed (links, function)
	- click on function names
	- goto previous expression
	
- New feature: external logging
	- settings managed through dBar bean managed bean properties:
		logDbPath		current	or <path to external db>		logs\logdb.nsf
		logEnabled		true/ false (defaults to false)
		logLevel		error, warn, info, debug				determines message types that are logged, will include all previous log types
		