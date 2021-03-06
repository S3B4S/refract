# Installation

Refract is available for a number of reactive programming libraries. For each library, a Refract integration is available for React, Inferno, Preact and Redux.

Available packages:

|  | [React](https://github.com/facebook/react) | [Inferno](https://infernojs.org/) | [Preact](https://preactjs.com/) | [Redux](https://github.com/reduxjs/redux) |
| :--- | :--- | :--- | :--- | :--- |
| [**Callbag**](https://github.com/callbag/callbag) | refract-callbag | refract-inferno-callbag | refract-preact-callbag | refract-redux-callbag |
| [**Most**](https://github.com/cujojs/most) | refract-most | refract-inferno-most | refract-preact-most | refract-redux-most |
| [**RxJS**](https://github.com/reactivex/rxjs) | refract-rxjs | refract-inferno-rxjs | refract-preact-rxjs | refract-redux-rxjs |
| [**xstream**](https://github.com/staltz/xstream) | refract-xstream | refract-inferno-xstream | refract-preact-xstream | refract-redux-xstream |

The examples below assume you're using `RxJS` - if you're using a different library, use the table above to find the correct package names.

## React, Inferno and Preact Packages

The React, Inferno and Preact packages don't require much set up - you just need to install the package \(usually via `npm` or `yarn`\):

```text
npm install --save refract-rxjs
```

The same applies to Inferno and Preact packages.

## Redux Packages

The Redux packages involve an extra step to apply the Refract enhancer to your Redux store:

1. Install the latest stable version \(again usually via `npm` or `yarn`\):

   ```text
   npm install --save refract-redux-rxjs
   ```

2. Import the Refract store enhancer and apply it to your redux store. This process is explained in detail in the Redux documentation: [Configuring your store](https://redux.js.org/recipes/configuring-your-store).

   For example:

   ```javascript
   import { compose, createStore } from 'redux'
   import { refractEnhancer } from 'refract-redux-rxjs'

   import reducers from './store'

   const store = createStore(reducers, {}, refractEnhancer())

   export default store
   ```

   _\(Note that this example is unrealistically simple!\)_

