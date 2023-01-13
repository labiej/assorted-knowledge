# Snippets for devtools

Modern browser come with built-in developer tools. These developer tools are powerful as is but can be improved further. Some frameworks released framework specific developer tools (e.g. Angular, react, …).

While these are definitely useful sometimes we want to execute some simple commands manually. Maybe we don't even use a framework or the information we want is not readily available. In this case it is possible to use the developer console to interact with the application.

A big annoyance is that larger sequences of such interactions are annoying to repeat. We could define a function but this is no longer available once the page is refreshed.

This can be easily resolved using snippets which can be found in the sources tab.
![[snippets.png.png]]

In this tab we can create JavaScript snippets (with specific names). These files can be executed whenever we want. So by converting the commands into a snippet they can be executed whenever we want.
By adding a function to the window object it becomes possible to run the command from the console multiple times. An example can be to check how the amount of a specific object evolves the longer the page is open. Inspecting the DOM after specific actions (number of children, total size, ...). 