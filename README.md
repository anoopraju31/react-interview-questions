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
        
   - *Disadvantage:* 
            1. The Virtual DOM can use more memory because it creates an additional representation of the DOM in memory.
