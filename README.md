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

  ## Virtual DOM

  https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270578#notes

  React checks for necessary DOM updates via a Virtual DOM.

It creates & compares virtual DOM snapshots to find out which parts of the rendered UI needs to be updated.
All components are reusible = > each component has its own isolated state
**But** React tracks state by component's type & position in the tree.
it's why the **key** is necessary. **Don't use index!!** in a map.
Keys are needed in list but not only: In order to re-execute a component, you add a key with a value changing.

## State Scheduling & Batching

When you call a state updating function (useState() => setMyState()),
the state update will not be executed instantly.
Instead, this will trigger a new component function execution
and the new state will be available afterwards

But because those state updates are scheduled
it is considered a best practice to perform state updates like this:

```
const [machin, setMachin] = useState(null);
function myUpdateMachin(newMachin){
    setMachin((prevMachin) => newMachin);
}
```

Because when using this approach here,
React guarantees you that here
you will always get the latest state snapshot available
and if multiple state updates of the same time
should be scheduled, they will be executed
in the order in which they were scheduled.
And you will always get the right value here.

## Optimizing React with MillionJS

https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/40270610#notes

https://million.dev/
