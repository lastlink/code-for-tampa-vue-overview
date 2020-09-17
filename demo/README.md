# demo

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Run your unit tests
```
yarn test:unit
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Init steps from scratch
* yarn and node must be installed
* `yarn global add @vue/cli`
* `vue create demo`
* preset: babel, typescript, postcss, pwa, router, vuex, unit-jest, eslint + prettier, separate config files
* add additional files and dependencies for junit
  * gitignore update
  * new scripts to package.json
    * `yarn add babel-plugin-require-context-hook jest-junit`
  * jest.config.js update
  * .jest/register-context.js
  * .vscode debug
* tailwind setup
    * `vue add tailwind`
    * import css in src/asset to main.ts
      * ```import "./assets/tailwind.css";```