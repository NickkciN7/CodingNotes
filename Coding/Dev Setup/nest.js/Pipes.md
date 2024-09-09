- decorate with @Injectable() decorator
- 2 typical use cases
	1. transformation
	2. validation
- on input to controller route handler
	- use into @Param decorator
		- @Param('id', ParseIntPipe) id: number
		- "binding the pipe at the method parameter level"
- validation
	- alternatives?
		- handle validation in route handler in controller?
			- break single responsibility principle (SRP)
		- validator class
			- would have to remember to call it everytime
		- middle ware
			- unaware of the execution context, including the handler that will be called and any of its parameters. Just has generic response and request objects