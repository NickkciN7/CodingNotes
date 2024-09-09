## create app
- `npx create-react-app my-app --template typescript` 
	- --template typescript will make it typescript based rather than js
	- npx: package runner tool. just like npm allows installing dependencies hosted on the registry, npx makes it easy to use CLI tools and other executables hosted on the registry
	- create-react-app
		- officially supported way to create single-page React applications
		- one of those executables hosted on the registry mentioned above
- can also do `npm init react-app my-app`
## create app with Vite
- `npm create vite@latest`
- this will give prompts. choose typescript and give project an appropriate name
- need to add eslint rule about not importing react (see section about Vite under eslint [[Eslint and Prettier]])
## run app
- `npm start` in the directory
	- `npm start` is a shortcut for `npm run start`, which runs the start script in the `package.json` file
