- @Module decorator
- provides meta data that Nest uses to organize the app structure
- every app has at least one module, the root module
	- starting point Nest uses to build app graph (internal datastructure Nest uses to resolve module and provider relationships)
- modules encapsulates providers by default, meaning impossible to inject providers that not part of current module or exported from imported modules. Can consider exported providers from module as module's public interface, or API
- modules are singleton by default
- @Global to make module global