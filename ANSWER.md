#### Lesson Challenge

Read these 4 articles: [Understanding the React Component Lifecycle](http://busypeoples.github.io/post/react-component-lifecycle/), [React component’s lifecycle](https://medium.com/react-ecosystem/react-components-lifecycle-ce09239010df), [Understanding React — Component life-cycle](https://medium.com/@baphemot/understanding-reactjs-component-life-cycle-823a640b3e8d), and [React JS: what is a PureComponent?](http://lucybain.com/blog/2018/react-js-pure-component/) and answer the following questions in the #explain-it channel:

1.  Describe what the in the workspace below will render on the screen and explain why.

All the components update the toggle every seccond except the 'Pure' component

2.  Describe a React anti-pattern that's used in the code.

Using this.setState({ toggle: true }); in App componentDidMount method trigging i re-render every 1 second

3.  How do we need to modify the `Normal3` Component in order to keep it from re-rendering if the `App` Component's state remains the same?

Add a shouldComponentUpdate method

This exercise is based on this sandbox: https://codesandbox.io/s/3vpp84yp5.

https://udacity-react.slack.com/archives/C9850EAA3/p1540144192000100

Luca [7:49 PM] / October 21st
Lesson 2.4.3 Challenge
*1) Describe what the code in the App.js file in the workspace below will render on the screen and explain why.*
The code in the App.js file renders a list of name and number for each component in the app, being the name the component name and the number the current amount of seconds.
At every second the app is re-render, updating the amount of seconds for every component.
However the Pure component won't be re-rendered and will keep on showing the initial amount of seconds. This because it extends the React PureComponent which does not implement shouldComponentUpdate().
A PureComponent in fact triggers a re-render with only a shallow props and sate comparison, meaning that it renders the same result given the same props and state.
This means that if pass a different prop using replacing
```this.setState({.toggle: true });```
with
```this.setState({ toggle: !this.state.toggle });```
then the Pure component will be re-rendered as well at every second updating the second amount.
*2) Describe a React anti-pattern that's used in the code.*
In the code, props are used in the state and this is mentioned by the React Docs as anti-pattern because it can lead to duplicates of "source of truth".
In fact the state is defined only when the component is first created, for example via the constructor, and it will refer to the props passed at that time to the component. However the component can receive new props when it is updated and this may not update the state accordingly.
Current best practise is to use the getDerivedStateFromProps static method in case we need to define a state using props, because this method is the first to be executed when a re-render occurs.
*3) Modify the Normal3 Component in order to keep it from re-rendering.*
By adding a shouldComponentUpdate method which always returns false.
```shouldComponentUpdate() {
      return false;
 }```