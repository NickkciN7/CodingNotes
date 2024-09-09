- articles referenced
	- https://shaifarfan.com/blog/airbnb-eslint-prettier-setup-react-typescript/
	- https://dev.to/rgolawski/how-to-make-eslint-and-prettier-work-together-2i5g
	- https://medium.com/globant/improving-code-quality-in-react-with-eslint-prettier-and-typescript-86635033d803
	- https://github.com/prettier/eslint-plugin-prettier the readme
- download the extensions in vs code for wsl
	- allows real time code warnings and allows formatting on save
	- change vs code settings to format on save
		- click ctrl+shift+p to bring up command runner, type settings and select "Open User Settings (JSON)"
		- enter these and save file. then restart vs code by closing or `ctrl+shift+p > reload window`
```

"editor.defaultFormatter": "esbenp.prettier-vscode",
"editor.formatOnSave": true,
"editor.codeActionsOnSave": {
	"source.fixAll.eslint": "explicit"
}
```

- also want in the dependencies of the project, not just vs code extensions, so that everyone who uses the code will have the same versions and we can set up rules for example to block a git commit until they fix warnings. Important when collabing with people so everyone has the same setup. Then vs code extensions will use the project settings.
## Eslint
- to have eslint as dev dependency in package.json type in terminal (while in the directory of your react project) `npm install eslint --save-dev` or `npm i -D eslint` 
	- dev depenencies are packages of code that only need to be used in the development phase, for example eslint shows bad code practices (but not necessarily illegal code) and we don't care about these warnings when we are running the app, it is only something that matters in the context of developing and typing code.
- initialize eslint
	- type `npx eslint --init`
	- choose the following options as they ask, this will create an `eslint.config.mjs` file
```
✔ How would you like to use ESLint? · To check syntax and find problems
✔ What type of modules does your project use? · JavaScript modules (import/export)
✔ Which framework does your project use? · react
✔ Does your project use TypeScript? · yes
✔ Where does your code run? · browser (in frontend but node in backend. whatever in root but delete the line related to browser/node in root and have the individual respective one in each package)
The config that you've selected requires the following dependencies:

eslint, globals, @eslint/js, typescript-eslint, eslint-plugin-react
✔ Would you like to install them now? · Yes
✔ Which package manager do you want to use? · npm
```
- could add scripts to the package.json to easily lint or attempt to fix the linting issues.
```
"lint": "eslint .", 
"lint:fix": "eslint . --fix",
```

- ignore files for linting, add this to export default
```
{ignores : ["eslint.config.mjs"]}
```

### Vite
- vite does not import React because it is using a newer version of react that automatically imports (https://kinsta.com/knowledgebase/react-must-be-in-scope-when-using-jsx/), however eslint is not smart enough to know that and gives warning in vite project
- to fix add this to the eslint.config.mjs
```
 {
    rules: {
      'react/react-in-jsx-scope': 'off',
    },
  },
```
## Prettier
- install as dev dependency
	- `npm i -D prettier`
- install dev dependencies that allow eslint and prettier to work together better
	- `npm i -D eslint-plugin-prettier eslint-config-prettier`
		- eslint-plugin-prettier
			- when eslint runs, it also triggers prettier
			- eslint then reports these prettier warnings as it normally reports its normal eslint warnings
		- eslint-config-prettier
			- disables all ESLint rules that might conflict with Prettier
- now we need to add to the eslint.config.mjs so that it uses these new dev dependencies
	- from https://github.com/prettier/eslint-plugin-prettier?tab=readme-ov-file#configuration-new-eslintconfigjs
	- "this plugin ships with an eslint-plugin-prettier/recommended config that sets up both eslint-plugin-prettier and eslint-config-prettier in one go. Import eslint-plugin-prettier/recommended and add it as the last item in the configuration array in your eslint.config.js file so that eslint-config-prettier has the opportunity to override other configs:"
	- We must import and add to the default export like (technically a bit different that above link as they are not using ECMAScript import but rather the old CommonJS require.' https://dev.to/rgolawski/how-to-make-eslint-and-prettier-work-together-2i5g shows it exactly as below )
```
import eslintPluginPrettierRecommended from "eslint-plugin-prettier/recommended";

export default [
  ...,
  eslintPluginPrettierRecommended,
];
```
- save and reload window. now if we mess up formatting with excessive spaces, it won't just format on save anymore, but will also give red squiggly lines
- we can set prettier rules by making a `.prettierrc.mjs` file in the root directory (same as `eslint.config.mjs`) and adding for example
```
export default {
  trailingComma: 'es5',
  tabWidth: 2,
  semi: true,
  singleQuote: true,
};
```

- ignore formatting on files by listing them in `.prettierignore`

## getting to work in mono repo
- redo steps above in frontend and backend
- backend/frontend already have some of those dependencies above installed and us running those commands (npm i -D eslint for example) updated the versions in package.json. however the package-lock.json's purpose is to lock versions of dependencies and dependencies of dependencies. we therefore need to update the package lock and run `npm update` at root to update the package-lock with the new versions. Otherwise our application will use the old versions specified in the package-lock.
-  reuse roots eslint in backend/frontend but give specific node or browser. for example backend. frontend do `...globals.browser` then delete the language options from the root config.
```
import globals from "globals";
import rootConfig from "../../eslint.config.mjs";

export default [
  ...rootConfig,
  { languageOptions: { globals: { ...globals.node } } },
];
```
- for prettier
```
import rootConfig from '../../.prettierrc.mjs';

export default { ...rootConfig };
```
