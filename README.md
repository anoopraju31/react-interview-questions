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
    - 
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
