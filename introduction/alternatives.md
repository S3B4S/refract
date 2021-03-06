# Alternatives

There are a number of alternative solutions for managing effects, most of which are focused on Redux. Typically, they allow you to observe actions dispatched to the store, and encourage you to only dispatch new actions as a side-effect. The most popular libraries are `redux-observable` and `redux-saga`.

There are also a number of libraries which offer ways to leverage Reactive programming with React, like `recompose` or `recycle`.

Refract takes a unique approach. It aims to provide a generalised approach to observing all data within your app, and managing any effects needed, by leveraging reactive programming. It colocates this logic with your components, which provides further advantages.

The benefits of Refract are:

1. **It can observe any source of data** - Component props, Redux actions, Redux state, any data source in your app.
2. **It can define any effect** - besides built-in effects \(mapping to props, replacing props and rendering\), you are fully in control of what can be done and how it is expressed.
3. **It colocates effects with your components** - they only run when your components run, which is great for code splitting and performance.
4. **It leverages existing reactive programming libraries** - you can choose from `RxJS`, `xstream`, `most`, and `callbag`, with no need to learn a domain-specific language. For each library, Refract provides strong type definitions.
5. **It doesn't prescribe a state container solution.**
6. **It uses React props for dependency injection.**

In our experience, Refract offers advantages in comparison to all libraries named below, with the exception of `redux-cycles`: Refract can achieve similar results to `redux-cycles`.

## redux-thunk

[Thunks](https://redux.js.org/api-reference/applymiddleware#example-using-thunk-middleware-for-async-actions) can be used to express any side-effect imperatively, and to dispatch to your store asynchronously.

It is a good way to get started before making a choice on what abstraction and side-effect model to use. There is nothing wrong in sticking to thunks!

## redux-saga

[Redux-saga](https://redux-saga.js.org/) is a powerful solution to express effects, and is the leader in its space.

However, like similar redux-based solutions, it is designed for observing actions and dispatching actions as a result, and other uses are either unsupported or discouraged. "Sagas" can be added dynamically, but they can't be removed.

Redux-saga introduces its own DSL and time-based operators. The learning curve is steep, it adds size to your project, and it is not re-usable outside Redux.

## redux-observable

[Redux-observable](https://redux-observable.js.org/) is similar to redux-saga and offers another powerful solution.

Like redux-saga, it is also designed for action-to-action effects. It is possible to dynamically add "epics", but it isn't possible to remove any.

It leverages RxJS for declaring effects, so the learning curve is also steep, and it is not re-usable outside Redux.

Redux-observable allows you to use other reactive libraries \(xstream, most\) but only on top of RxJS, which is unfortunately included by default.

## redux-loop

[Redux-loop](https://redux-loop.js.org/) embeds side-effect logic in your reducers.

It is not limited to reacting to actions and you can also react to state changes. However, effects can only be actions, and it adds complexity to your reducers. It comes with the disadvantage of not separating concerns of state mutation and side-effects. It is also inherently tied to Redux.

Redux-loop is not as powerful as redux-saga or redux-observable with time-based effects.

## redux-cycles

[Redux-cycles](https://github.com/cyclejs-community/redux-cycles) is a Cycle.js-based solution which adds Redux observability. It benefits from the mighty power of Cycle.js and its declarative and reactive architecture. It leverages reactive programming and can be used with various libraries \(most, RxJS, xstream\), but requires xstream by default.

## react-side-effect

[React-side-effect](https://github.com/gaearon/react-side-effect) allows declarative side-effects within React, by reacting to prop changes. It is a great solution for basic needs. While it shares similarities with Refract, it cannot react to prop functions being called. It is also not able to create time-based effects, and side-effects can't use props \(no dependency injection\).

## recycle

[Recycle](https://github.com/recyclejs/recycle) is an abstraction built on top of React which enables the use of reactive programming \(RxJS\) for handling state and effects.

## recompose

[Recompose](https://github.com/acdlite/recompose/blob/master/docs/API.md) is a React library providing various higher-order components and utilities. The HoCs provided by recompose are specialised and allow to manipulate props and handle state. It offers observable utilities to handle props and rendering reactively.

