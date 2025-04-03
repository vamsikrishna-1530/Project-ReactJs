
**Interviewer:** Can you explain the differences between Props and State in ReactJS?

**Candidate:** Sure, I'd be happy to explain the differences.

- **Props:**
  - Props, short for properties, are used to pass data from a parent component to a child component.
  - Props are immutable, meaning they cannot be changed by the child component receiving them.
  - Props help make components reusable. You can pass different data to the same component to render different outputs.
  - Example of using props: 
    ```jsx
    function Greeting(props) {
      return <h1>Hello, {props.name}!</h1>;
    }
    
    <Greeting name="John" />
    ```

- **State:**
  - State is a built-in object that allows components to create and manage their own data.
  - State is mutable and can change over time, often as a result of user actions or network responses.
  - When the state changes, the component re-renders to reflect the new state.
  - State is typically managed within the component itself, using the `useState` hook in functional components or `this.state` in class components.
  - Example of using state:
    ```jsx
    function Counter() {
      const [count, setCount] = useState(0);

      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>
            Click me
          </button>
        </div>
      );
    }
    ```
  
To summarize:
- Props are immutable and passed from parent to child, used for rendering dynamic data.
- State is mutable and managed within the component, used for handling data that changes over time.

**Interviewer:** Great explanation! Thank you.
