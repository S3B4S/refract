# withEffects

Used to enhance a plain component, wrapping it in a WithEffects component which handles side-effects internally. It is a curried higher-order component.

## Packages

`withEffects` is provided by our React, Inferno or Preact packages - `refract-*`, `refract-inferno-*`, `refract-preact-*`.

## Signature

```javascript
withEffects = (
    handler,
    errorHandler?,
    Context?
) => aperture => BaseComponent => {
    return WrappedComponent
}
```

## Arguments

1. `handler` _\(function\)_: a function which causes side-effects in response to `effect` values.

   Signature: `(initialProps, initialContext) => (effect) => { /* handle effect here */ }`

   * The `initialProps` are all props passed into the `WrappedComponent`.
   * The `initialContext` is the initial context value of the provided `Context` \(see below, React &gt;= 16.6.0 only\)
   * The `effect` is each value emitted by your `aperture`.
   * Within the body of the function, you cause any side-effect you wish.

2. `errorHandler` _\(function\)_: an _optional_ function for catching any unexpected errors thrown within your `aperture`. Typically used for logging errors.

   Signature: `(initialProps, initialContext) => (error) => { /* handle error here */ }`

   * The `initialProps` are all props passed into the `WrappedComponent`.
   * The `initialContext` is the initial context value of the provided `Context` \(see below, React &gt;= 16.6.0 only\)
   * The `error` is each value emitted by your `aperture`.
   * Within the body of the function, you cause any side-effect you wish.

3. `Context` _\(ReactContext\)_: a React Context object. Its initial value will be passed to `handler`, `errorHandler` and `aperture` \(React 16.6.0 and above only\).
4. `aperture` _\(function\)_: a function which observes data sources within your app, passes this data through any necessary logic flows, and outputs a stream of `effect` values in response.

   Signature: `(initialProps, initialContext) => (component) => { return effectStream }`.

   * The `initialProps` are all props passed into the `WrappedComponent`.
   * The `initialContext` is the initial context value of the provided `Context` \(see above, React &gt;= 16.6.0 only\)
   * The `component` is an object which lets you observe your React, Inferno or Preact component: see [Observing React](../usage/observing-react.md)
   * Within the body of the function, you observe the event source you choose, pipe the events through your stream library of choice, and return a single stream of effects.

5. `BaseComponent` _\(React component\)_: any react component.

## Returns

`WrappedComponent` _\(React component\)_: a new component which contains your side-effect logic, and which will render your component as per usual.

## Example

```javascript
import { withEffects } from 'refract-rxjs'

const BaseComponent = ({ username, onChange }) => (
    <input value={username} onChange={onChange} />
)

const aperture = initialProps => component => {
    return component.observe('username').pipe(
        debounce(2000),
        map(username => ({
            type: 'localstorage',
            name: 'username',
            value: username
        }))
    )
}

const handler = initialProps => effect => {
    switch (effect.type) {
        case 'localstorage':
            localstorage.setItem(effect.name, effect.value)
            return
    }
}

const WrappedComponent = withEffects(handler)(aperture)(BaseComponent)
```

## Tips

* Take a look at our recipe for [dependency injection](../recipes/dependency-injection.md) into your Refract components.
* `withEffects` is curried so that you can re-use a bound `handler` \(and `errorHandler`\) with multiple different `apertures`.

