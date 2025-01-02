- monorepo management
	- mono repo is just a repository containing multiple packages, in our case backend and frontend
- install
	- `npm install -g lerna`
- initialize monorepo
	- `lerna init`
- make a folder called "packages" in the root directory that will host backend and frontend
- tell lerna where we will have our packages by adding this to lerna.json (and package.json if not there)
	- `"packages": ["packages/*"]`
- can add scripts to run backend or frontend or build all for example
```
 "scripts": {

    "start:frontend": "lerna run start --scope=frontend",

    "start:backend": "lerna run start --scope=backend",

    "build:all": "lerna run build"

  },
```
