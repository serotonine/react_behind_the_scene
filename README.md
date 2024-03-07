# React behind the scenes

https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270506#questions

## How does React update the DOM ?

(App as tree ok)
https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270524#questions

## 4 Ways to improve performance

- ### memo()

=> will take a look at your **component** and evaluate if the previous prop value === the current prop value. If yes memo prevents the execution of the component function.

```
const Counter = memo(function Counter({...props}){
    ....
    return(<markup>);
});
export default Counter;
```

**Don't overuse memo()**
Use it **as high up in the component tree** as possible.
Because:

- if a component is prevented from execution all its child will not be executed either.
- Checking props with memo() **cost performance**
- Dont use memo() on components which props change frequently.

- ### A clever component composition.

https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270540#notes
Child component execution does not trigger parent execution.
So the best is to gather all logic bounds to this component in it.

- ### useCallBack()

Once again when a function is executed it is in fact recreated (another JS reference).
So useCallBack() prevents a function to be recreated.

- ### useMemo()
  Same than memo() but for **normal functions**
  Should only used for complex calculations functions.
  ```
  const initialCountIsPrime = useMemo(() => isPrime(initialCount), [initialCount]);
  ```
  **Don't overuse useMemo()**
