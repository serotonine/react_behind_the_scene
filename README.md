# React behind the scenes

https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270506#questions

## How does React update the DOM ?

(App as tree ok)
https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270524#questions

## 3 Ways to improve performance

### memo

=> will take a look at your component and evaluate if the previous prop value === the current prop value. If yes memo prevents the execution of the function/component.

```
const Counter = memo(function Counter({...props}){
    ....
    return(<markup>);
});
export default Counter;
```

**_ Don't overuse memo()_**
Use it **_ as high up in the component tree _** as possible.
Because:

- if a component is prevented from execution all its child will not be executed either.
- Checking props with memo() **_ cost performance _**
- Dont use memo() on components which props change frequently.

### A clever component composition.

https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270540#notes
Child component execution does not trigger parent execution.
So the best is to gather all logic bounds to a component in this component.
