# Writing Tests
- At the moment, Dark does not provide an out of the box testing framework. However, it's fairly straightforward to write tests using REPLs and Crons.

- Will Dark support testing?
	- Dark will have integrated unit testing for fns and handlers. We plan to generate tests for you based on types, and to trivially allow you to turn past requests into unit tests.
	- It should also be possible to run integration tests that interact well with Dark - we plan to build features that support this use case.

- You can write logic to check that the printed messages say exactly what we want them to without having to read every message. In this example, a portion of the message that gets printed when the name is not long enough has been accidentally deleted so a warning is displayed.
	...what?

- a few ideas for hacks:
	- cron that collects failing tests and notifies team
	- custom dashboard
