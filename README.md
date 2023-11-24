# React Interview Questions 
- A List of React Interview Questions and their answers. 

## Questions

1. **What is React and how can you best describe it?**
   - React is a JavaScript Library for building User Interface.
        
2. **What is JSX?**
   - JSX stands for JavaScript XML.
   - JSX is simply a syntax extension of JavaScript.
   - JSX looks similar to HTML, it returns JavaScript Object which when rendered generates HTML.
   - JSX was developed to make developer experience easier.
   - Earlier we used function createElement() for React to create a template, which returns React Elements, an object representation of a DOM node. This Becomes really hard to track by developers as it gets nested inside one another.
   - Both JS Engine and Browser does not  understand JSX directly, it needs to be transpiled (converting one code to another code) before reaching the JS Engine.
        
3. **What is the Virtual DOM and how is it used by React?**
   - A virtual DOM is a lightweight JavaScript representation of the Document Object Model (DOM).
   - Basically, it's a virtual representation of DOM using a nested JavaScript Object (nested React Element).
   - React Uses Virtual DOM to update the actual DOM.
   - React uses a Diff Algorithm to compares the virtual DOM of previous state and the current state and find out the difference in Vitual DOM and re-renders nesscary the Component and then updates the Actual DOM.        
   - Disadvantage:
      - The Virtual DOM can use more memory because it creates an additional representation of the DOM in memory.
            
4. **What is the difference between Controlled and Uncontrolled inputs?**
    - Controlled Inputs are the inputs who value is controlled by the state of the component and change to the value is handled by React component methods.
      
    ``` javascript
     import React, { useState } from 'react';

     function ControlledInputExample() {
       const [inputValue, setInputValue] = useState('');
     
       const handleChange = (e) => {
         setInputValue(e.target.value);
       };
     
       return (
         <input
           type="text"
           value={inputValue}
           onChange={handleChange}
         />
       );
     }

    ```

   - In this example, the inputValue state is used to control the value of the text input. The handleChange function updates the state whenever the input value changes.
    
   - Uncontrolled Inputs on the other hand, does not store its value in the React component's state. Instead, the value is managed by the DOM itself. We typically use refs to interact with the DOM and get the current value when needed.
    
    ``` javascript
    import React, { useRef } from 'react';

    function UncontrolledInputExample() {
      const inputRef = useRef();
    
      const handleClick = () => {
        // Access the current value of the input using the ref
        alert(`Input value: ${inputRef.current.value}`);
      };
    
      return (
        <div>
          <input type="text" ref={inputRef} />
          <button onClick={handleClick}>Get Input Value</button>
        </div>
      );
    }

    ```
    - In this example, the ref (inputRef) is used to get the current value of the input when the button is clicked. The value is not stored in the component's state.

5. **What are some of the hooks commonly used in React?**
    - Hook is a special function that allows functional components to access and interact with React features such as state and lifecycle methods.
    - The most commonly used hooks are *useState*, *useEffect*, *useRef*, *useMemo* and *useCallback*.
    - useState: It is a function that enables functional components to declare and manage state variables, providing a way to hold and update state within the component, with the returned array containing the current state value and a function to modify it.
    - useEffect: It is used to perform side effects in functional components, such as data fetching, subscriptions, or manually changing the DOM, and it runs after every render.
    - useRef: It is used to create a mutable object that persists across renders and can be used to store and access values without causing re-renders, commonly used for accessing and interacting with the DOM.
    - useMemo: It is used to memoize the result of a computation, preventing unnecessary recalculation of values during renders and optimizing performance by caching the result until the dependencies change.
    - useCallback: It is used to memoize and obtain a memoized version of a callback function, preventing unnecessary re-creation of the function on each render and optimizing performance by caching the callback until the specified dependencies change.
   
6. **What is useMemo and how does it works?**
    - useMemo is a React hook that is used to memoize the result of a function so that it's not recomputed on every render. 
    - This can be useful in when a function's result depends on some inputs, and those inputs are expensive to compute.
    - useMemo ensures that the function is only recomputed when its dependencies change.
    - useMemo takes two arguments: the function to memoize and an array of dependencies.
    - The array of dependencies determines when the memoized function should be recomputed.
    - If any of the dependencies change between renders, the memoized function is recalculated; otherwise, the cached result is used.
    ``` javascript
    import React, { useMemo, useState } from 'react';
    
    function ExpensiveCalculationComponent({ a, b }) {
      const expensiveResult = useMemo(() => {
        // Perform some expensive calculation based on inputs a and b
        console.log('Calculating...');
        return a + b;
      }, [a, b]); // Dependencies: a and b
    
      return (
        <div>
          <p>Result: {expensiveResult}</p>
        </div>
      );
    }
    
    function App() {
      const [valueA, setValueA] = useState(5);
      const [valueB, setValueB] = useState(10);
    
      return (
        <div>
          <ExpensiveCalculationComponent a={valueA} b={valueB} />
          <button onClick={() => setValueA(valueA + 1)}>Increment A</button>
          <button onClick={() => setValueB(valueB + 1)}>Increment B</button>
        </div>
      );
    }

    ```
    
7. **What is useCallback and how does it works?**
   - useCallback is a React hook that memoizes a callback function, preventing it from being recreated on each render unless its dependencies change.
   - This is useful in when passing callbacks to child components could result in unnecessary re-renders of those child components.
   - useCallback ensures that the callback function is the same between renders unless the specified dependencies change.
   - useCallback memoizes the provided callback function
   - Memoization means that the same function reference is returned as long as the specified dependencies remain unchanged.
   - useCallback takes two arguments: the callback function to memoize and an array of dependencies.
   - The array of dependencies determines when the callback function should be recomputed.
   - If any of the dependencies change between renders, the memoized callback is recalculated; otherwise, the cached function reference is used.
    ``` javascript
    import React, { useCallback, useState } from 'react';
    
    function ChildComponent({ onClick }) {
      console.log('ChildComponent is rendered.');
      return <button onClick={onClick}>Click me</button>;
    }
    
    function ParentComponent() {
      const [count, setCount] = useState(0);
    
      // Without useCallback:
      // const handleClick = () => {
      //   console.log('Button clicked!');
      //   setCount(count + 1);
      // };
    
      // With useCallback:
      const handleClick = useCallback(() => {
        console.log('Button clicked!');
        setCount((prevCount) => prevCount + 1);
      }, [setCount]);
    
      console.log('ParentComponent is rendered.');
    
      return (
        <div>
          <p>Count: {count}</p>
          <ChildComponent onClick={handleClick} />
        </div>
      );
    }
    
    function App() {
      return <ParentComponent />;
    }

    ```
8. **What is the difference between useState and useRef?**

   | Feature                   | `useState`                               | `useRef`                                 |
   |---------------------------|------------------------------------------|------------------------------------------|
   | **Purpose**               | Manage state in functional components    | Create mutable objects, often for DOM interactions or holding values without causing re-renders   |
   | **Re-renders**            | Changes trigger re-renders               | Changes do not trigger re-renders         |
   | **Updating Values**       | Use state variable and `setState` function | Directly update `.current` property of the `ref` object |
   | **Initialization**        | Requires initial state value             | Can be initialized with or without an initial value |
   | **Use Cases**             | Managing stateful data that causes re-renders | Accessing and interacting with the DOM, holding values without re-renders |
   | **Example**               | `const [count, setCount] = useState(0);` | `const myRef = useRef(initialValue);`    |

9. **What is Context and how does it works?**
    - In React, Context is a feature that allows you to pass data through the component tree without having to pass props down manually at every level.


10. **What is Props Drilling?** 
    - Props drilling, also known as "prop passing" or "prop threading," refers to the situation in a React application where you need to pass data through several layers of nested components by explicitly providing them as props. 
    - This can occur when a deeply nested component needs access to data that is originally located in a higher-level ancestor component.
    - ![Prop Drilling](https://res.cloudinary.com/practicaldev/image/fetch/s--YWOuVoW6--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sx5c2nw5nideoz5vqe8q.png)
    ``` JSX
    // Top-level component
    const App = () => {
      const data = /* some data */;
    
      return (
        <div>
          <ComponentA data={data} />
        </div>
      );
    };
    
    // ComponentA
    const ComponentA = ({ data }) => {
      return (
        <div>
          <ComponentB data={data} />
        </div>
      );
    };
    
    // ComponentB
    const ComponentB = ({ data }) => {
      return (
        <div>
          <ComponentC data={data} />
        </div>
      );
    };
    
    // ComponentC
    const ComponentC = ({ data }) => {
      // Access and use the data
      return (
        <div>
          {data}
        </div>
      );
    };

    ```
