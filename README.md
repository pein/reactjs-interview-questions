## Core React

1.  ### What is React?

    React (aka React.js or ReactJS) is an **open-source front-end JavaScript library** that is used for building composable user interfaces, especially for single-page applications. It is used for handling view layer for web and mobile apps based on components in a declarative approach.

    React was created by [Jordan Walke](https://github.com/jordwalke), a software engineer working for Facebook. React was first deployed on Facebook's News Feed in 2011 and on Instagram in 2012.

2.  ### What is the history behind React evolution?

    The history of ReactJS started in 2010 with the creation of **XHP**. XHP is a PHP extension which improved the syntax of the language such that XML document fragments become valid PHP expressions and the primary purpose was used to create custom and reusable HTML elements.

    The main principle of this extension was to make front-end code easier to understand and to help avoid cross-site scripting attacks. The project was successful to prevent the malicious content submitted by the scrubbing user.

    But there was a different problem with XHP in which dynamic web applications require many roundtrips to the server, and XHP did not solve this problem. Also, the whole UI was re-rendered for small change in the application. Later, the initial prototype of React is created with the name **FaxJ** by Jordan inspired from XHP. Finally after sometime React has been introduced as a new library into JavaScript world.

    **Note:** JSX comes from the idea of XHP

3.  ### What are the major features of React?

    The major features of React are:

    - Uses **JSX** syntax, a syntax extension of JS that allows developers to write HTML in their JS code.
    - It uses **Virtual DOM** instead of Real DOM considering that Real DOM manipulations are expensive.
    - Supports **server-side rendering** which is useful for Search Engine Optimizations(SEO).
    - Follows **Unidirectional or one-way** data flow or data binding.
    - Uses **reusable/composable** UI components to develop the view.

4.  ### What is JSX?

    _JSX_ stands for _JavaScript XML_ and it is an XML-like syntax extension to ECMAScript. Basically it just provides the syntactic sugar for the `React.createElement(type, props, ...children)` function, giving us expressiveness of JavaScript along with HTML like template syntax.

    In the example below, the text inside `<h1>` tag is returned as JavaScript function to the render function.

    ```jsx harmony
    export default function App() {
      return <h1 className="greeting">{"Hello, this is a JSX Code!"}</h1>;
    }
    ```

    If you don't use JSX syntax then the respective JavaScript code should be written as below,

    ```javascript
    import { createElement } from "react";

    export default function App() {
      return createElement(
        "h1",
        { className: "greeting" },
        "Hello, this is a JSX Code!"
      );
    }
    ```

     <details><summary><b>See Class</b></summary>
     <p>

    ```jsx harmony
    class App extends React.Component {
      render() {
        return <h1 className="greeting">{"Hello, this is a JSX Code!"}</h1>;
      }
    }
    ```

     </p>
     </details>

    **Note:** JSX is stricter than HTML

5.  ### What is the difference between Element and Component?

    An _Element_ is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. _Elements_ can contain other _Elements_ in their props. Creating a React element is cheap. Once an element is created, it cannot be mutated.

    The JavaScript representation(Without JSX) of React Element would be as follows:

    ```javascript
    const element = React.createElement("div", { id: "login-btn" }, "Login");
    ```

    and this element can be simiplified using JSX

    ```html
    <div id="login-btn">Login</div>
    ```

    The above `React.createElement()` function returns an object as below:

    ```javascript
    {
      type: 'div',
      props: {
        children: 'Login',
        id: 'login-btn'
      }
    }
    ```

    Finally, this element renders to the DOM using `ReactDOM.render()`.

    Whereas a **component** can be declared in several different ways. It can be a class with a `render()` method or it can be defined as a function. In either case, it takes props as an input, and returns a JSX tree as the output:

    ```javascript
    const Button = ({ handleLogin }) => (
      <div id={"login-btn"} onClick={handleLogin}>
        Login
      </div>
    );
    ```

    Then JSX gets transpiled to a `React.createElement()` function tree:

    ```javascript
    const Button = ({ handleLogin }) =>
      React.createElement(
        "div",
        { id: "login-btn", onClick: handleLogin },
        "Login"
      );
    ```

6.  ### How to create components in React?

    Components are the building blocks of creating User Interfaces(UI) in React. There are two possible ways to create a component.

    1. **Function Components:** This is the simplest way to create a component. Those are pure JavaScript functions that accept props object as the one and only one parameter and return React elements to render the output:

       ```jsx harmony
       function Greeting({ message }) {
         return <h1>{`Hello, ${message}`}</h1>;
       }
       ```

    2. **Class Components:** You can also use ES6 class to define a component. The above function component can be written as a class component:

       ```jsx harmony
       class Greeting extends React.Component {
         render() {
           return <h1>{`Hello, ${this.props.message}`}</h1>;
         }
       }
       ```

7.  ### When to use a Class Component over a Function Component?

    After the addition of Hooks(i.e. React 16.8 onwards) it is always recommended to use Function components over Class components in React. Because you could use state, lifecycle methods and other features that were only available in class component present in function component too.

    But even there are two reasons to use Class components over Function components.

    1. If you need a React functionality whose Function component equivalent is not present yet, like Error Boundaries.
    2. In older versions, If the component needs _state or lifecycle methods_ then you need to use class component.

    So the summary to this question is as follows:

    **Use Function Components:**

    - If you don't need state or lifecycle methods, and your component is purely presentational.
    - For simplicity, readability, and modern code practices, especially with the use of React Hooks for state and side effects.

    **Use Class Components:**

    - If you need to manage state or use lifecycle methods.
    - In scenarios where backward compatibility or integration with older code is necessary.

    **Note:** You can also use reusable [react error boundary](https://github.com/bvaughn/react-error-boundary) third-party component without writing any class. i.e, No need to use class components for Error boundaries.

    The usage of Error boundaries from the above library is quite straight forward.

    > **_Note when using react-error-boundary:_** ErrorBoundary is a client component. You can only pass props to it that are serializable or use it in files that have a `"use client";` directive.

    ```jsx
    "use client";

    import { ErrorBoundary } from "react-error-boundary";

    <ErrorBoundary fallback={<div>Something went wrong</div>}>
      <ExampleApplication />
    </ErrorBoundary>;
    ```

8.  ### What are Pure Components?

    Pure components are the components which render the same output for the same state and props. In function components, you can achieve these pure components through memoized `React.memo()` API wrapping around the component. This API prevents unnecessary re-renders by comparing the previous props and new props using shallow comparison. So it will be helpful for performance optimizations.

    But at the same time, it won't compare the previous state with the current state because function component itself prevents the unnecessary rendering by default when you set the same state again.

    The syntactic representation of memoized components looks like below,

    ```jsx
    const MemoizedComponent = memo(SomeComponent, arePropsEqual?);
    ```

    Below is the example of how child component(i.e., EmployeeProfile) prevents re-renders for the same props passed by parent component(i.e.,EmployeeRegForm).

    ```jsx
    import { memo, useState } from "react";

    const EmployeeProfile = memo(function EmployeeProfile({ name, email }) {
      return (
        <>
          <p>Name:{name}</p>
          <p>Email: {email}</p>
        </>
      );
    });
    export default function EmployeeRegForm() {
      const [name, setName] = useState("");
      const [email, setEmail] = useState("");
      return (
        <>
          <label>
            Name:{" "}
            <input value={name} onChange={(e) => setName(e.target.value)} />
          </label>
          <label>
            Email:{" "}
            <input value={email} onChange={(e) => setEmail(e.target.value)} />
          </label>
          <hr />
          <EmployeeProfile name={name} />
        </>
      );
    }
    ```

    In the above code, the email prop has not been passed to child component. So there won't be any re-renders for email prop change.

    In class components, the components extending _`React.PureComponent`_ instead of _`React.Component`_ become the pure components. When props or state changes, _PureComponent_ will do a shallow comparison on both props and state by invoking `shouldComponentUpdate()` lifecycle method.

    **Note:** `React.memo()` is a higher-order component.

9.  ### What is state in React?

    _State_ of a component is an object that holds some information that may change over the lifetime of the component. The important point is whenever the state object changes, the component re-renders. It is always recommended to make our state as simple as possible and minimize the number of stateful components.

    ![state](images/state.jpg)

    Let's take an example of **User** component with `message` state. Here, **useState** hook has been used to add state to the User component and it returns an array with current state and function to update it.

    ```jsx harmony
    import { useState } from "react";

    function User() {
      const [message, setMessage] = useState("Welcome to React world");

      return (
        <div>
          <h1>{message}</h1>
        </div>
      );
    }
    ```

    Whenever React calls your component or access `useState` hook, it gives you a snapshot of the state for that particular render.

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    import React from "react";
    class User extends React.Component {
      constructor(props) {
        super(props);

        this.state = {
          message: "Welcome to React world",
        };
      }

      render() {
        return (
          <div>
            <h1>{this.state.message}</h1>
          </div>
        );
      }
    }
    ```

    </p>
    </details>

    State is similar to props, but it is private and fully controlled by the component ,i.e., it is not accessible to any other component till the owner component decides to pass it.

10. ### What are props in React?

    _Props_ are inputs to components. They are single values or objects containing a set of values that are passed to components on creation similar to HTML-tag attributes. Here, the data is passed down from a parent component to a child component.

    The primary purpose of props in React is to provide following component functionality:

    1. Pass custom data to your component.
    2. Trigger state changes.
    3. Use via `this.props.reactProp` inside component's `render()` method.

    For example, let us create an element with `reactProp` property:

    ```jsx harmony
    <Element reactProp={"1"} />
    ```

    This `reactProp` (or whatever you came up with) attribute name then becomes a property attached to React's native props object which originally already exists on all components created using React library.

    ```jsx harmony
    props.reactProp;
    ```

    For example, the usage of props in function component looks like below:

    ```jsx
    import React from "react";
    import ReactDOM from "react-dom";

    const ChildComponent = (props) => {
      return (
        <div>
          <p>{props.name}</p>
          <p>{props.age}</p>
          <p>{props.gender}</p>
        </div>
      );
    };

    const ParentComponent = () => {
      return (
        <div>
          <ChildComponent name="John" age="30" gender="male" />
          <ChildComponent name="Mary" age="25" geneder="female" />
        </div>
      );
    };
    ```

The properties from props object can be accessed directly using destructing feature from ES6 (ECMAScript 2015). It is also possible to fallback to default value when the prop value is not specified. The above child component can be simplified like below.

```jsx harmony
const ChildComponent = ({ name, age, gender = "male" }) => {
  return (
    <div>
      <p>{name}</p>
      <p>{age}</p>
      <p>{gender}</p>
    </div>
  );
};
```

**Note:** The default value won't be used if you pass `null` or `0` value. i.e, default value is only used if the prop value is missed or `undefined` value has been passed.

  <details><summary><b>See Class</b></summary>
     The Props accessed in Class Based Component as below

```jsx
import React from "react";
import ReactDOM from "react-dom";

class ChildComponent extends React.Component {
  render() {
    return (
      <div>
        <p>{this.props.name}</p>
        <p>{this.props.age}</p>
        <p>{this.props.gender}</p>
      </div>
    );
  }
}

class ParentComponent extends React.Component {
  render() {
    return (
      <div>
        <ChildComponent name="John" age="30" gender="male" />
        <ChildComponent name="Mary" age="25" gender="female" />
      </div>
    );
  }
}
```

  </details>

11. ### What is the difference between state and props?

    In React, both `state` and `props` are plain JavaScript objects and used to manage the data of a component, but they are used in different ways and have different characteristics.

    The `state` entity is managed by the component itself and can be updated using the setter(`setState()` for class components) function. Unlike props, state can be modified by the component and is used to manage the internal state of the component. i.e, state acts as a component's memory. Moreover, changes in the state trigger a re-render of the component and its children. The components cannot become reusable with the usage of state alone.

    On the otherhand, `props` (short for "properties") are passed to a component by its parent component and are `read-only`, meaning that they cannot be modified by the own component itself. i.e, props acts as arguments for a function. Also, props can be used to configure the behavior of a component and to pass data between components. The components become reusable with the usage of props.

12. ### What is the difference between HTML and React event handling?

    Below are some of the main differences between HTML and React event handling,

    1. In HTML, the event name usually represents in _lowercase_ as a convention:

       ```html
       <button onclick="activateLasers()"></button>
       ```

       Whereas in React it follows _camelCase_ convention:

       ```jsx harmony
       <button onClick={activateLasers}>
       ```

    2. In HTML, you can return `false` to prevent default behavior:

       ```html
       <a
         href="#"
         onclick='console.log("The link was clicked."); return false;'
       />
       ```

       Whereas in React you must call `preventDefault()` explicitly:

       ```javascript
       function handleClick(event) {
         event.preventDefault();
         console.log("The link was clicked.");
       }
       ```

    3. In HTML, you need to invoke the function by appending `()`
       Whereas in react you should not append `()` with the function name. (refer "activateLasers" function in the first point for example)

13. ### What are synthetic events in React?

    `SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers. The native events can be accessed directly from synthetic events using `nativeEvent` attribute.

    Let's take an example of BookStore title search component with the ability to get all native event properties

    ```js
    function BookStore() {
      function handleTitleChange(e) {
        console.log("The new title is:", e.target.value);
        // 'e' represents synthetic event
        const nativeEvent = e.nativeEvent;
        console.log(nativeEvent);
        e.stopPropagation();
        e.preventDefault();
      }

      return <input name="title" onChange={handleTitleChange} />;
    }
    ```

14. ### What are inline conditional expressions?

    You can use either _if statements_ or _ternary expressions_ which are available from JS to conditionally render expressions. Apart from these approaches, you can also embed any expressions in JSX by wrapping them in curly braces and then followed by JS logical operator `&&`.

    ```jsx harmony
    <h1>Hello!</h1>;
    {
      messages.length > 0 && !isLogin ? (
        <h2>You have {messages.length} unread messages.</h2>
      ) : (
        <h2>You don't have unread messages.</h2>
      );
    }
    ```

15. ### What is "key" prop and what is the benefit of using it in arrays of elements?

    A `key` is a special attribute you **should** include when mapping over arrays to render data. _Key_ prop helps React identify which items have changed, are added, or are removed.

    Keys should be unique among its siblings. Most often we use ID from our data as _key_:

    ```jsx harmony
    const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
    ```

    When you don't have stable IDs for rendered items, you may use the item _index_ as a _key_ as a last resort:

    ```jsx harmony
    const todoItems = todos.map((todo, index) => (
      <li key={index}>{todo.text}</li>
    ));
    ```

    **Note:**

    1. Using _indexes_ for _keys_ is **not recommended** if the order of items may change. This can negatively impact performance and may cause issues with component state.
    2. If you extract list item as separate component then apply _keys_ on list component instead of `li` tag.
    3. There will be a warning message in the console if the `key` prop is not present on list items.
    4. The key attribute accepts either string or number and internally convert it as string type.
    5. Don't generate the key on the fly something like `key={Math.random()}`. Because the keys will never match up between re-renders and DOM created everytime.

16. ### What is Virtual DOM?

    The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.

17. ### How Virtual DOM works?

    The _Virtual DOM_ works in three simple steps.

    1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.

       ![vdom](images/vdom1.png)

    2. Then the difference between the previous DOM representation and the new one is calculated.

       ![vdom2](images/vdom2.png)

    3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

       ![vdom3](images/vdom3.png)

18. ### What is the difference between Shadow DOM and Virtual DOM?

    The _Shadow DOM_ is a browser technology designed primarily for scoping variables and CSS in _web components_. The _Virtual DOM_ is a concept implemented by libraries in JavaScript on top of browser APIs.

19. ### What is React Fiber?

    Fiber is the new _reconciliation_ engine or reimplementation of core algorithm in React v16. The goal of React Fiber is to increase its suitability for areas like animation, layout, gestures, ability to pause, abort, or reuse work and assign priority to different types of updates; and new concurrency primitives.

20. ### What is the main goal of React Fiber?

    The goal of _React Fiber_ is to increase its suitability for areas like animation, layout, and gestures. Its headline feature is **incremental rendering**: the ability to split rendering work into chunks and spread it out over multiple frames.

    _from documentation_

    Its main goals are:

    1. Ability to split interruptible work in chunks.
    2. Ability to prioritize, rebase and reuse work in progress.
    3. Ability to yield back and forth between parents and children to support layout in React.
    4. Ability to return multiple elements from render().
    5. Better support for error boundaries.

21. ### What are controlled components?

    A component that controls the input elements within the forms on subsequent user input is called **Controlled Component**, i.e, every state mutation will have an associated handler function. That means, the displayed data is always in sync with the state of the component.

    The controlled components will be implemented using the below steps,

    1. Initialize the state using use state hooks in function components or inside constructor for class components.
    2. Set the value of the form element to the respective state variable.
    3. Create an event handler to handle the user input changes through useState updater function or setState from class component.
    4. Attach the above event handler to form elements change or click events

    For example, the name input field updates the user name using `handleChange` event handler as below,

    ```javascript
    import React, { useState } from "react";

    function UserProfile() {
      const [username, setUsername] = useState("");

      const handleChange = (e) => {
        setUsername(e.target.value);
      };

      return (
        <form>
          <label>
            Name:
            <input type="text" value={username} onChange={handleChange} />
          </label>
        </form>
      );
    }
    ```

22. ### What are uncontrolled components?

    The **Uncontrolled Components** are the ones that store their own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.

    The uncontrolled components will be implemented using the below steps,

    1. Create a ref using useRef react hook in function component or `React.createRef()` in class based component.
    2. Attach this ref to the form element.
    3. The form element value can be accessed directly through `ref` in event handlers or `componentDidMount` for class components

    In the below UserProfile component, the `username` input is accessed using ref.

    ```jsx harmony
    import React, { useRef } from "react";

    function UserProfile() {
      const usernameRef = useRef(null);

      const handleSubmit = (event) => {
        event.preventDefault();
        console.log("The submitted username is: " + usernameRef.current.value);
      };

      return (
        <form onSubmit={handleSubmit}>
          <label>
            Username:
            <input type="text" ref={usernameRef} />
          </label>
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```

    In most cases, it's recommend to use controlled components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    class UserProfile extends React.Component {
      constructor(props) {
        super(props);
        this.handleSubmit = this.handleSubmit.bind(this);
        this.input = React.createRef();
      }

      handleSubmit(event) {
        alert("A name was submitted: " + this.input.current.value);
        event.preventDefault();
      }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <label>
              {"Name:"}
              <input type="text" ref={this.input} />
            </label>
            <input type="submit" value="Submit" />
          </form>
        );
      }
    }
    ```

    </p>
    </details>

23. ### What is the difference between createElement and cloneElement?

    JSX elements will be transpiled to `React.createElement()` functions to create React elements which are going to be used for the object representation of UI. Whereas `cloneElement` is used to clone an element and pass it new props.

24. ### What is Lifting State Up in React?

    When several components need to share the same changing data then it is recommended to _lift the shared state up_ to their closest common ancestor. That means if two child components share the same data from its parent, then move the state to parent instead of maintaining local state in both of the child components.

25. ### What are Higher-Order Components?

    A _higher-order component_ (_HOC_) is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

    We call them **pure components** because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

    ```javascript
    const EnhancedComponent = higherOrderComponent(WrappedComponent);
    ```

    HOC can be used for many use cases:

    1. Code reuse, logic and bootstrap abstraction.
    2. Render hijacking.
    3. State abstraction and manipulation.
    4. Props manipulation.

26. ### What is children prop?

    _Children_ is a prop that allows you to pass components as data to other components, just like any other prop you use. Component tree put between component's opening and closing tag will be passed to that component as `children` prop.

    A simple usage of children prop looks as below,

    ```jsx harmony
    function MyDiv({ children }){
        return (
          <div>
            {children}
          </div>;
        );
    }

    export default function Greeting() {
      return (
        <MyDiv>
          <span>{"Hello"}</span>
          <span>{"World"}</span>
        </MyDiv>
      );
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>

    ```jsx harmony
    const MyDiv = React.createClass({
      render: function () {
        return <div>{this.props.children}</div>;
      },
    });

    ReactDOM.render(
      <MyDiv>
        <span>{"Hello"}</span>
        <span>{"World"}</span>
      </MyDiv>,
      node
    );
    ```

    </p>
    </details>

    **Note:** There are several methods available in the legacy React API to work with this prop. These include `React.Children.map`, `React.Children.forEach`, `React.Children.count`, `React.Children.only`, `React.Children.toArray`.

27. ### How to write comments in React?

    The comments in React/JSX are similar to JavaScript Multiline comments but are wrapped in curly braces.

    **Single-line comments:**

    ```jsx harmony
    <div>
      {/* Single-line comments(In vanilla JavaScript, the single-line comments are represented by double slash(//)) */}
      {`Welcome ${user}, let's play React`}
    </div>
    ```

    **Multi-line comments:**

    ```jsx harmony
    <div>
      {/* Multi-line comments for more than
       one line */}
      {`Welcome ${user}, let's play React`}
    </div>
    ```

28. ### What is reconciliation?

    `Reconciliation` is the process through which React updates the Browser DOM and makes React work faster. React use a `diffing algorithm` so that component updates are predictable and faster. React would first calculate the difference between the `real DOM` and the copy of DOM `(Virtual DOM)` when there's an update of components.
    React stores a copy of Browser DOM which is called `Virtual DOM`. When we make changes or add data, React creates a new Virtual DOM and compares it with the previous one. This comparison is done by `Diffing Algorithm`.
    Now React compares the Virtual DOM with Real DOM. It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called _Reconciliation_.

29. ### Does the lazy function support named exports?

    No, currently `React.lazy` function supports default exports only. If you would like to import modules which are named exports, you can create an intermediate module that reexports it as the default. It also ensures that tree shaking keeps working and don’t pull unused components.
    Let's take a component file which exports multiple named components,

    ```javascript
    // MoreComponents.js
    export const SomeComponent = /* ... */;
    export const UnusedComponent = /* ... */;
    ```

    and reexport `MoreComponents.js` components in an intermediate file `IntermediateComponent.js`

    ```javascript
    // IntermediateComponent.js
    export { SomeComponent as default } from "./MoreComponents.js";
    ```

    Now you can import the module using lazy function as below,

    ```javascript
    import React, { lazy } from "react";
    const SomeComponent = lazy(() => import("./IntermediateComponent.js"));
    ```

30. ### Why React uses `className` over `class` attribute?

    The attribute names written in JSX turned into keys of JavaScript objects and the JavaScript names cannot contain dashes or reserved words, it is recommended to use camelCase wherever applicable in JSX code. The attribute `class` is a keyword in JavaScript, and JSX is an extension of JavaScript. That's the principle reason why React uses `className` instead of `class`. Pass a string as the `className` prop.

    ```jsx harmony
    render() {
      return <span className="menu navigation-menu">{'Menu'}</span>
    }
    ```

31. ### What are fragments?

    It's a common pattern or practice in React for a component to return multiple elements. _Fragments_ let you group a list of children without adding extra nodes to the DOM.
    You need to use either `<Fragment>` or a shorter syntax having empty tag (`<></>`).

    Below is the example of how to use fragment inside _Story_ component.

    ```jsx harmony
    function Story({ title, description, date }) {
      return (
        <Fragment>
          <h2>{title}</h2>
          <p>{description}</p>
          <p>{date}</p>
        </Fragment>
      );
    }
    ```

    It is also possible to render list of fragments inside a loop with the mandatory **key** attribute supplied.

    ```jsx harmony
    function StoryBook() {
      return stories.map((story) => (
        <Fragment key={story.id}>
          <h2>{story.title}</h2>
          <p>{story.description}</p>
          <p>{story.date}</p>
        </Fragment>
      ));
    }
    ```

    Usually, you don't need to use `<Fragment>` until there is a need of _key_ attribute. The usage of shorter syntax looks like below.

    ```jsx harmony
    function Story({ title, description, date }) {
      return (
        <>
          <h2>{title}</h2>
          <p>{description}</p>
          <p>{date}</p>
        </>
      );
    }
    ```

32. ### Why fragments are better than container divs?

    Below are the list of reasons to prefer fragments over container DOM elements,

    1. Fragments are a bit faster and use less memory by not creating an extra DOM node. This only has a real benefit on very large and deep trees.
    2. Some CSS mechanisms like _Flexbox_ and _CSS Grid_ have a special parent-child relationships, and adding divs in the middle makes it hard to keep the desired layout.
    3. The DOM Inspector is less cluttered.

33. ### What are portals in React?

    _Portal_ is a recommended way to render children into a DOM node that exists outside the DOM hierarchy of the parent component. When using
    CSS transform in a component, its descendant elements should not use fixed positioning, otherwise the layout will blow up.

    ```javascript
    ReactDOM.createPortal(child, container);
    ```

    The first argument is any render-able React child, such as an element, string, or fragment. The second argument is a DOM element.

34. ### What are stateless components?

    If the behaviour of a component is independent of its state then it can be a stateless component. You can use either a function or a class for creating stateless components. But unless you need to use a lifecycle hook in your components, you should go for function components. There are a lot of benefits if you decide to use function components here; they are easy to write, understand, and test, a little faster, and you can avoid the `this` keyword altogether.

35. ### What are stateful components?

    If the behaviour of a component is dependent on the _state_ of the component then it can be termed as stateful component. These _stateful components_ are either function components with hooks or _class components_.

    Let's take an example of function stateful component which update the state based on click event,

    ```javascript
    import React, {useState} from 'react';

    const App = (props) => {
    const [count, setCount] = useState(0);
    handleIncrement() {
      setCount(count+1);
    }

    return (
      <>
        <button onClick={handleIncrement}>Increment</button>
        <span>Counter: {count}</span>
      </>
      )
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>
    The equivalent class stateful component with a state that gets initialized in the `constructor`.

    ```jsx harmony
    class App extends Component {
      constructor(props) {
        super(props);
        this.state = { count: 0 };
      }

      handleIncrement() {
        setState({ count: this.state.count + 1 });
      }

      render() {
        <>
          <button onClick={() => this.handleIncrement}>Increment</button>
          <span>Count: {count}</span>
        </>;
      }
    }
    ```

    </p>
    </details>

36. ### How to apply validation on props in React?

    When the application is running in _development mode_, React will automatically check all props that we set on components to make sure they have _correct type_. If the type is incorrect, React will generate warning messages in the console. It's disabled in _production mode_ due to performance impact. The mandatory props are defined with `isRequired`.

    The set of predefined prop types:

    1. `PropTypes.number`
    2. `PropTypes.string`
    3. `PropTypes.array`
    4. `PropTypes.object`
    5. `PropTypes.func`
    6. `PropTypes.node`
    7. `PropTypes.element`
    8. `PropTypes.bool`
    9. `PropTypes.symbol`
    10. `PropTypes.any`

    We can define `propTypes` for `User` component as below:

    ```jsx harmony
    import React from "react";
    import PropTypes from "prop-types";

    class User extends React.Component {
      static propTypes = {
        name: PropTypes.string.isRequired,
        age: PropTypes.number.isRequired,
      };

      render() {
        return (
          <>
            <h1>{`Welcome, ${this.props.name}`}</h1>
            <h2>{`Age, ${this.props.age}`}</h2>
          </>
        );
      }
    }
    ```

    **Note:** In React v15.5 _PropTypes_ were moved from `React.PropTypes` to `prop-types` library.

    _The Equivalent Functional Component_

    ```jsx harmony
    import React from "react";
    import PropTypes from "prop-types";

    function User({ name, age }) {
      return (
        <>
          <h1>{`Welcome, ${name}`}</h1>
          <h2>{`Age, ${age}`}</h2>
        </>
      );
    }

    User.propTypes = {
      name: PropTypes.string.isRequired,
      age: PropTypes.number.isRequired,
    };
    ```

37. ### What are the advantages of React?

    Below are the list of main advantages of React,

    1. Increases the application's performance with _Virtual DOM_.
    2. JSX makes code easy to read and write.
    3. It renders both on client and server side (_SSR_).
    4. Easy to integrate with frameworks (Angular, Backbone) since it is only a view library.
    5. Easy to write unit and integration tests with tools such as Jest.

38. ### What are the limitations of React?

    Apart from the advantages, there are few limitations of React too,

    1. React is just a view library, not a full framework.
    2. There is a learning curve for beginners who are new to web development.
    3. Integrating React into a traditional MVC framework requires some additional configuration.
    4. The code complexity increases with inline templating and JSX.
    5. Too many smaller components leading to over engineering or boilerplate.

39. ### What are the recommended ways for static type checking?

    Normally we use _PropTypes library_ (`React.PropTypes` moved to a `prop-types` package since React v15.5) for _type checking_ in the React applications. For large code bases, it is recommended to use _static type checkers_ such as Flow or TypeScript, that perform type checking at compile time and provide auto-completion features.

40. ### What is the use of `react-dom` package?

    The `react-dom` package provides _DOM-specific methods_ that can be used at the top level of your app. Most of the components are not required to use this module. Some of the methods of this package are:

    1. `render()`
    2. `hydrate()`
    3. `unmountComponentAtNode()`
    4. `findDOMNode()`
    5. `createPortal()`

41. ### What is ReactDOMServer?

    The `ReactDOMServer` object enables you to render components to static markup (typically used on node server). This object is mainly used for _server-side rendering_ (SSR). The following methods can be used in both the server and browser environments:

    1. `renderToString()`
    2. `renderToStaticMarkup()`

    For example, you generally run a Node-based web server like Express, Hapi, or Koa, and you call `renderToString` to render your root component to a string, which you then send as response.

    ```javascript
    // using Express
    import { renderToString } from "react-dom/server";
    import MyPage from "./MyPage";

    app.get("/", (req, res) => {
      res.write(
        "<!DOCTYPE html><html><head><title>My Page</title></head><body>"
      );
      res.write('<div id="content">');
      res.write(renderToString(<MyPage />));
      res.write("</div></body></html>");
      res.end();
    });
    ```

42. ### How to use innerHTML in React?

    The `dangerouslySetInnerHTML` attribute is React's replacement for using `innerHTML` in the browser DOM. Just like `innerHTML`, it is risky to use this attribute considering cross-site scripting (XSS) attacks. You just need to pass a `__html` object as key and HTML text as value.

    In this example MyComponent uses `dangerouslySetInnerHTML` attribute for setting HTML markup:

    ```jsx harmony
    function createMarkup() {
      return { __html: "First &middot; Second" };
    }

    function MyComponent() {
      return <div dangerouslySetInnerHTML={createMarkup()} />;
    }
    ```

43. ### How to use styles in React?

    The `style` attribute accepts a JavaScript object with camelCased properties rather than a CSS string. This is consistent with the DOM style JavaScript property, is more efficient, and prevents XSS security holes.

    ```jsx harmony
    const divStyle = {
      color: "blue",
      backgroundImage: "url(" + imgUrl + ")",
    };

    function HelloWorldComponent() {
      return <div style={divStyle}>Hello World!</div>;
    }
    ```

    Style keys are camelCased in order to be consistent with accessing the properties on DOM nodes in JavaScript (e.g. `node.style.backgroundImage`).

44. ### How events are different in React?

    Handling events in React elements has some syntactic differences:

    1. React event handlers are named using camelCase, rather than lowercase.
    2. With JSX you pass a function as the event handler, rather than a string.

45. ### What is the impact of indexes as keys?

    Keys should be stable, predictable, and unique so that React can keep track of elements.

    In the below code snippet each element's key will be based on ordering, rather than tied to the data that is being represented. This limits the optimizations that React can do and creates confusing bugs in the application.

    ```jsx harmony
    {
      todos.map((todo, index) => <Todo {...todo} key={index} />);
    }
    ```

    If you use element data for unique key, assuming `todo.id` is unique to this list and stable, React would be able to reorder elements without needing to reevaluate them as much.

    ```jsx harmony
    {
      todos.map((todo) => <Todo {...todo} key={todo.id} />);
    }
    ```

    **Note:** If you don't specify `key` prop at all, React will use index as a key's value while iterating over an array of data.

46. ### How do you conditionally render components?

    In some cases you want to render different components depending on some state. JSX does not render `false` or `undefined`, so you can use conditional _short-circuiting_ to render a given part of your component only if a certain condition is true.

    ```jsx harmony
    const MyComponent = ({ name, address }) => (
      <div>
        <h2>{name}</h2>
        {address && <p>{address}</p>}
      </div>
    );
    ```

    If you need an `if-else` condition then use _ternary operator_.

    ```jsx harmony
    const MyComponent = ({ name, address }) => (
      <div>
        <h2>{name}</h2>
        {address ? <p>{address}</p> : <p>{"Address is not available"}</p>}
      </div>
    );
    ```

47. ### Why we need to be careful when spreading props on DOM elements?

    When we _spread props_ we run into the risk of adding unknown HTML attributes, which is a bad practice. Instead we can use prop destructuring with `...rest` operator, so it will add only required props.

    For example,

    ```jsx harmony
    const ComponentA = () => (
      <ComponentB isDisplay={true} className={"componentStyle"} />
    );

    const ComponentB = ({ isDisplay, ...domProps }) => (
      <div {...domProps}>{"ComponentB"}</div>
    );
    ```

48. ### How do you memoize a component?

    There are memoize libraries available which can be used on function components.

    For example `moize` library can memoize the component in another component.

    ```jsx harmony
    import moize from "moize";
    import Component from "./components/Component"; // this module exports a non-memoized component

    const MemoizedFoo = moize.react(Component);

    const Consumer = () => {
      <div>
        {"I will memoize the following entry:"}
        <MemoizedFoo />
      </div>;
    };
    ```

    **Update:** Since React v16.6.0, we have a `React.memo`. It provides a higher order component which memoizes component unless the props change. To use it, simply wrap the component using React.memo before you use it.

    ```js
    const MemoComponent = React.memo(function MemoComponent(props) {
      /* render using props */
    });
    OR;
    export default React.memo(MyFunctionComponent);
    ```

49. ### How you implement Server Side Rendering or SSR?

    React is already equipped to handle rendering on Node servers. A special version of the DOM renderer is available, which follows the same pattern as on the client side.

    ```jsx harmony
    import ReactDOMServer from "react-dom/server";
    import App from "./App";

    ReactDOMServer.renderToString(<App />);
    ```

    This method will output the regular HTML as a string, which can be then placed inside a page body as part of the server response. On the client side, React detects the pre-rendered content and seamlessly picks up where it left off.

50. ### How to enable production mode in React?

    You should use Webpack's `DefinePlugin` method to set `NODE_ENV` to `production`, by which it strip out things like propType validation and extra warnings. Apart from this, if you minify the code, for example, Uglify's dead-code elimination to strip out development only code and comments, it will drastically reduce the size of your bundle.

51. ### Do Hooks replace render props and higher order components?

    Both render props and higher-order components render only a single child but in most of the cases Hooks are a simpler way to serve this by reducing nesting in your tree.

52. ### What is a switching component?

    A _switching component_ is a component that renders one of many components. We need to use object to map prop values to components.

    For example, a switching component to display different pages based on `page` prop:

    ```jsx harmony
    import HomePage from "./HomePage";
    import AboutPage from "./AboutPage";
    import ServicesPage from "./ServicesPage";
    import ContactPage from "./ContactPage";

    const PAGES = {
      home: HomePage,
      about: AboutPage,
      services: ServicesPage,
      contact: ContactPage,
    };

    const Page = (props) => {
      const Handler = PAGES[props.page] || ContactPage;

      return <Handler {...props} />;
    };

    // The keys of the PAGES object can be used in the prop types to catch dev-time errors.
    Page.propTypes = {
      page: PropTypes.oneOf(Object.keys(PAGES)).isRequired,
    };
    ```

53. ### What are React Mixins?

    _Mixins_ are a way to totally separate components to have a common functionality. Mixins **should not be used** and can be replaced with _higher-order components_ or _decorators_.

    One of the most commonly used mixins is `PureRenderMixin`. You might be using it in some components to prevent unnecessary re-renders when the props and state are shallowly equal to the previous props and state:

    ```javascript
    const PureRenderMixin = require("react-addons-pure-render-mixin");

    const Button = React.createClass({
      mixins: [PureRenderMixin],
      // ...
    });
    ```

     <!-- TODO: mixins are deprecated -->

54. ### What are the Pointer Events supported in React?

    _Pointer Events_ provide a unified way of handling all input events. In the old days we had a mouse and respective event listeners to handle them but nowadays we have many devices which don't correlate to having a mouse, like phones with touch surface or pens. We need to remember that these events will only work in browsers that support the _Pointer Events_ specification.

    The following event types are now available in _React DOM_:

    1. `onPointerDown`
    2. `onPointerMove`
    3. `onPointerUp`
    4. `onPointerCancel`
    5. `onGotPointerCapture`
    6. `onLostPointerCapture`
    7. `onPointerEnter`
    8. `onPointerLeave`
    9. `onPointerOver`
    10. `onPointerOut`

55. ### Why should component names start with capital letter?

    If you are rendering your component using JSX, the name of that component has to begin with a capital letter otherwise React will throw an error as an unrecognized tag. This convention is because only HTML elements and SVG tags can begin with a lowercase letter.

    ```jsx harmony
    function SomeComponent {
      // Code goes here
    }
    ```

    You can define function component whose name starts with lowercase letter, but when it's imported it should have a capital letter. Here lowercase is fine:

    ```jsx harmony
    function myComponent {
      render() {
        return <div />;
      }
    }

    export default myComponent;
    ```

    While when imported in another file it should start with capital letter:

    ```jsx harmony
    import MyComponent from "./myComponent";
    ```

56. ### Are custom DOM attributes supported in React v16?

    Yes. In the past, React used to ignore unknown DOM attributes. If you wrote JSX with an attribute that React doesn't recognize, React would just skip it.

    For example, let's take a look at the below attribute:

    ```jsx harmony
    <div mycustomattribute={"something"} />
    ```

    Would render an empty div to the DOM with React v15:

    ```html
    <div />
    ```

    In React v16 any unknown attributes will end up in the DOM:

    ```html
    <div mycustomattribute="something" />
    ```

    This is useful for supplying browser-specific non-standard attributes, trying new DOM APIs, and integrating with opinionated third-party libraries.

57. ### How to loop inside JSX?

    You can simply use `Array.prototype.map` with ES6 _arrow function_ syntax.

    For example, the `items` array of objects is mapped into an array of components:

    ```jsx harmony
    <tbody>
      {items.map((item) => (
        <SomeComponent key={item.id} name={item.name} />
      ))}
    </tbody>
    ```

    But you can't iterate using `for` loop:

    ```jsx harmony
    <tbody>
      for (let i = 0; i < items.length; i++) {
        <SomeComponent key={items[i].id} name={items[i].name} />
      }
    </tbody>
    ```

    This is because JSX tags are transpiled into _function calls_, and you can't use statements inside expressions. This may change thanks to `do` expressions which are _stage 1 proposal_.

58. ### How do you access props in attribute quotes?

    React (or JSX) doesn't support variable interpolation inside an attribute value. The below representation won't work:

    ```jsx harmony
    <img className="image" src="images/{this.props.image}" />
    ```

    But you can put any JS expression inside curly braces as the entire attribute value. So the below expression works:

    ```jsx harmony
    <img className="image" src={"images/" + this.props.image} />
    ```

    Using _template strings_ will also work:

    ```jsx harmony
    <img className="image" src={`images/${this.props.image}`} />
    ```

59. ### What is React proptype array with shape?

    If you want to pass an array of objects to a component with a particular shape then use `React.PropTypes.shape()` as an argument to `React.PropTypes.arrayOf()`.

    ```javascript
    ReactComponent.propTypes = {
      arrayWithShape: React.PropTypes.arrayOf(
        React.PropTypes.shape({
          color: React.PropTypes.string.isRequired,
          fontSize: React.PropTypes.number.isRequired,
        })
      ).isRequired,
    };
    ```

60. ### How to conditionally apply class attributes?

    You shouldn't use curly braces inside quotes because it is going to be evaluated as a string.

    ```jsx harmony
    <div className="btn-panel {this.props.visible ? 'show' : 'hidden'}">
    ```

    Instead you need to move curly braces outside (don't forget to include spaces between class names):

    ```jsx harmony
    <div className={'btn-panel ' + (this.props.visible ? 'show' : 'hidden')}>
    ```

    _Template strings_ will also work:

    ```jsx harmony
    <div className={`btn-panel ${this.props.visible ? 'show' : 'hidden'}`}>
    ```

61. ### What is the difference between React and ReactDOM?

    The `react` package contains `React.createElement()`, `React.Component`, `React.Children`, and other helpers related to elements and component classes. You can think of these as the isomorphic or universal helpers that you need to build components. The `react-dom` package contains `ReactDOM.render()`, and in `react-dom/server` we have _server-side rendering_ support with `ReactDOMServer.renderToString()` and `ReactDOMServer.renderToStaticMarkup()`.

62. ### Why ReactDOM is separated from React?

    The React team worked on extracting all DOM-related features into a separate library called _ReactDOM_. React v0.14 is the first release in which the libraries are split. By looking at some of the packages, `react-native`, `react-art`, `react-canvas`, and `react-three`, it has become clear that the beauty and essence of React has nothing to do with browsers or the DOM.

    To build more environments that React can render to, React team planned to split the main React package into two: `react` and `react-dom`. This paves the way to writing components that can be shared between the web version of React and React Native.

63. ### How to use React label element?

    If you try to render a `<label>` element bound to a text input using the standard `for` attribute, then it produces HTML missing that attribute and prints a warning to the console.

    ```jsx harmony
    <label for={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

    Since `for` is a reserved keyword in JavaScript, use `htmlFor` instead.

    ```jsx harmony
    <label htmlFor={'user'}>{'User'}</label>
    <input type={'text'} id={'user'} />
    ```

64. ### How to combine multiple inline style objects?

    You can use _spread operator_ in regular React:

    ```jsx harmony
    <button style={{ ...styles.panel.button, ...styles.panel.submitButton }}>
      {"Submit"}
    </button>
    ```

    If you're using React Native then you can use the array notation:

    ```jsx harmony
    <button style={[styles.panel.button, styles.panel.submitButton]}>
      {"Submit"}
    </button>
    ```

65. ### How to re-render the view when the browser is resized?

    You can use the `useState` hook to manage the width and height state variables, and the `useEffect` hook to add and remove the `resize` event listener. The `[]` dependency array passed to useEffect ensures that the effect only runs once (on mount) and not on every re-render.

    ```javascript
    import React, { useState, useEffect } from "react";
    function WindowDimensions() {
      const [dimensions, setDimensions] = useState({
        width: window.innerWidth,
        height: window.innerHeight,
      });

      useEffect(() => {
        function handleResize() {
          setDimensions({
            width: window.innerWidth,
            height: window.innerHeight,
          });
        }
        window.addEventListener("resize", handleResize);
        return () => window.removeEventListener("resize", handleResize);
      }, []);

      return (
        <span>
          {dimensions.width} x {dimensions.height}
        </span>
      );
    }
    ```

    <details>
    <summary><h4>Using Class Component</h4></summary>

    You can listen to the `resize` event in `componentDidMount()` and then update the dimensions (`width` and `height`). You should remove the listener in `componentWillUnmount()` method.

    ```javascript
    class WindowDimensions extends React.Component {
      constructor(props) {
        super(props);
        this.updateDimensions = this.updateDimensions.bind(this);
      }

      componentWillMount() {
        this.updateDimensions();
      }

      componentDidMount() {
        window.addEventListener("resize", this.updateDimensions);
      }

      componentWillUnmount() {
        window.removeEventListener("resize", this.updateDimensions);
      }

      updateDimensions() {
        this.setState({
          width: window.innerWidth,
          height: window.innerHeight,
        });
      }

      render() {
        return (
          <span>
            {this.state.width} x {this.state.height}
          </span>
        );
      }
    }
    ```

    </details>

66. ### How to pretty print JSON with React?

    We can use `<pre>` tag so that the formatting of the `JSON.stringify()` is retained:

    ```jsx harmony
    const data = { name: "John", age: 42 };

    function User {
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
    }

    const container = createRoot(document.getElementById("container"));

    container.render(<User />);
    ```

      <details><summary><b>See Class</b></summary>
      <p>

    ```jsx harmony
    const data = { name: "John", age: 42 };

    class User extends React.Component {
      render() {
        return <pre>{JSON.stringify(data, null, 2)}</pre>;
      }
    }

    React.render(<User />, document.getElementById("container"));
    ```

      </p>
      </details>

67. ### Why you can't update props in React?

    The React philosophy is that props should be _immutable_(read only) and _top-down_. This means that a parent can send any prop values to a child, but the child can't modify received props.

68. ### How to focus an input element on page load?

    You need to use `useEffect` hook to set focus on input field during page load time for functional component.

    ```jsx harmony
    import React, { useEffect, useRef } from "react";

    const App = () => {
      const inputElRef = useRef(null);

      useEffect(() => {
        inputElRef.current.focus();
      }, []);

      return (
        <div>
          <input defaultValue={"Won't focus"} />
          <input ref={inputElRef} defaultValue={"Will focus"} />
        </div>
      );
    };

    ReactDOM.render(<App />, document.getElementById("app"));
    ```

      <details><summary><b>See Class</b></summary>
      <p>
      You can do it by creating _ref_ for `input` element and using it in `componentDidMount()`:

    ```jsx harmony
    class App extends React.Component {
      componentDidMount() {
        this.nameInput.focus();
      }

      render() {
        return (
          <div>
            <input defaultValue={"Won't focus"} />
            <input
              ref={(input) => (this.nameInput = input)}
              defaultValue={"Will focus"}
            />
          </div>
        );
      }
    }

    ReactDOM.render(<App />, document.getElementById("app"));
    ```

      </p>
      </details>

69. ### How can we find the version of React at runtime in the browser?

    You can use `React.version` to get the version.

    ```jsx harmony
    const REACT_VERSION = React.version;

    ReactDOM.render(
      <div>{`React version: ${REACT_VERSION}`}</div>,
      document.getElementById("app")
    );
    ```

70. ### How to add Google Analytics for React Router?

    Add a listener on the `history` object to record each page view:

    ```javascript
    history.listen(function (location) {
      window.ga("set", "page", location.pathname + location.search);
      window.ga("send", "pageview", location.pathname + location.search);
    });
    ```

71. ### How do you apply vendor prefixes to inline styles in React?

    React _does not_ apply _vendor prefixes_ automatically. You need to add vendor prefixes manually.

    ```jsx harmony
    <div
      style={{
        transform: "rotate(90deg)",
        WebkitTransform: "rotate(90deg)", // note the capital 'W' here
        msTransform: "rotate(90deg)", // 'ms' is the only lowercase vendor prefix
      }}
    />
    ```

72. ### How to import and export components using React and ES6?

    You should use default for exporting the components

    ```jsx harmony
    import User from "user";

    export default function MyProfile {
        return <User type="customer">//...</User>;
    }
    ```

    <details><summary><b>See Class</b></summary>
    <p>
     ```jsx harmony
     import React from "react";
     import User from "user";

    export default class MyProfile extends React.Component {
    render() {
    return <User type="customer">//...</User>;
    }
    }

    ```
    </p>
    </details>

    With the export specifier, the MyProfile is going to be the member and exported to this module and the same can be imported without mentioning the name in other components.
    ```

73. ### What are the exceptions on React component naming?

    The component names should start with an uppercase letter but there are few exceptions to this convention. The lowercase tag names with a dot (property accessors) are still considered as valid component names.
    For example, the below tag can be compiled to a valid component,

    ```jsx harmony
         render() {
              return (
                <obj.component/> // `React.createElement(obj.component)`
              )
        }
    ```

74. ### Is it possible to use async/await in plain React?

    If you want to use `async`/`await` in React, you will need _Babel_ and [transform-async-to-generator](https://babeljs.io/docs/en/babel-plugin-transform-async-to-generator) plugin. React Native ships with Babel and a set of transforms.

75. ### What are the common folder structures for React?

    There are two common practices for React project file structure.

    1.  **Grouping by features or routes:**

        One common way to structure projects is locate CSS, JS, and tests together, grouped by feature or route.

        ```
        common/
        ├─ Avatar.js
        ├─ Avatar.css
        ├─ APIUtils.js
        └─ APIUtils.test.js
        feed/
        ├─ index.js
        ├─ Feed.js
        ├─ Feed.css
        ├─ FeedStory.js
        ├─ FeedStory.test.js
        └─ FeedAPI.js
        profile/
        ├─ index.js
        ├─ Profile.js
        ├─ ProfileHeader.js
        ├─ ProfileHeader.css
        └─ ProfileAPI.js
        ```

    2.  **Grouping by file type:**

        Another popular way to structure projects is to group similar files together.

        ```
        api/
        ├─ APIUtils.js
        ├─ APIUtils.test.js
        ├─ ProfileAPI.js
        └─ UserAPI.js
        components/
        ├─ Avatar.js
        ├─ Avatar.css
        ├─ Feed.js
        ├─ Feed.css
        ├─ FeedStory.js
        ├─ FeedStory.test.js
        ├─ Profile.js
        ├─ ProfileHeader.js
        └─ ProfileHeader.css
        ```

76. ### What are the popular packages for animation?

    _React Transition Group_ and _React Motion_ are popular animation packages in React ecosystem.

77. ### What is the benefit of styles modules?

    It is recommended to avoid hard coding style values in components. Any values that are likely to be used across different UI components should be extracted into their own modules.

    For example, these styles could be extracted into a separate component:

    ```javascript
    export const colors = {
      white,
      black,
      blue,
    };

    export const space = [0, 8, 16, 32, 64];
    ```

    And then imported individually in other components:

    ```javascript
    import { space, colors } from "./styles";
    ```

78. ### What are the popular React-specific linters?

    ESLint is a popular JavaScript linter. There are plugins available that analyse specific code styles. One of the most common for React is an npm package called `eslint-plugin-react`. By default, it will check a number of best practices, with rules checking things from keys in iterators to a complete set of prop types.

    Another popular plugin is `eslint-plugin-jsx-a11y`, which will help fix common issues with accessibility. As JSX offers slightly different syntax to regular HTML, issues with `alt` text and `tabindex`, for example, will not be picked up by regular plugins.

## React Router

79. ### What is React Router?

    React Router is a powerful routing library built on top of React that helps you add new screens and flows to your application incredibly quickly, all while keeping the URL in sync with what's being displayed on the page.

80. ### How React Router is different from history library?

    React Router is a wrapper around the `history` library which handles interaction with the browser's `window.history` with its browser and hash histories. It also provides memory history which is useful for environments that don't have global history, such as mobile app development (React Native) and unit testing with Node.

81. ### What are the `<Router>` components of React Router v6?

    React Router v6 provides below 4 `<Router>` components:

    1.  `<BrowserRouter>`:Uses the HTML5 history API for standard web apps.
    2.  `<HashRouter>`:Uses hash-based routing for static servers.
    3.  `<MemoryRouter>`:Uses in-memory routing for testing and non-browser environments.
    4.  `<StaticRouter>`:Provides static routing for server-side rendering (SSR).

    The above components will create _browser_, _hash_, _memory_ and _static_ history instances. React Router v6 makes the properties and methods of the `history` instance associated with your router available through the context in the `router` object.

82. ### What is the purpose of `push()` and `replace()` methods of `history`?

    A history instance has two methods for navigation purpose.

    1.  `push()`
    2.  `replace()`

    If you think of the history as an array of visited locations, `push()` will add a new location to the array and `replace()` will replace the current location in the array with the new one.

83. ### How do you programmatically navigate using React Router v4?

    There are three different ways to achieve programmatic routing/navigation within components.

    1.  **Using the `withRouter()` higher-order function:**

        The `withRouter()` higher-order function will inject the history object as a prop of the component. This object provides `push()` and `replace()` methods to avoid the usage of context.

        ```jsx harmony
        import { withRouter } from "react-router-dom"; // this also works with 'react-router-native'

        const Button = withRouter(({ history }) => (
          <button
            type="button"
            onClick={() => {
              history.push("/new-location");
            }}
          >
            {"Click Me!"}
          </button>
        ));
        ```

    2.  **Using `<Route>` component and render props pattern:**

        The `<Route>` component passes the same props as `withRouter()`, so you will be able to access the history methods through the history prop.

        ```jsx harmony
        import { Route } from "react-router-dom";

        const Button = () => (
          <Route
            render={({ history }) => (
              <button
                type="button"
                onClick={() => {
                  history.push("/new-location");
                }}
              >
                {"Click Me!"}
              </button>
            )}
          />
        );
        ```

    3.  **Using context:**

        This option is not recommended and treated as unstable API.

        ```jsx harmony
        const Button = (props, context) => (
          <button
            type="button"
            onClick={() => {
              context.history.push("/new-location");
            }}
          >
            {"Click Me!"}
          </button>
        );

        Button.contextTypes = {
          history: React.PropTypes.shape({
            push: React.PropTypes.func.isRequired,
          }),
        };
        ```

84. ### How to get query parameters in React Router v4?

    The ability to parse query strings was taken out of React Router v4 because there have been user requests over the years to support different implementation. So the decision has been given to users to choose the implementation they like. The recommended approach is to use query strings library.

    ```javascript
    const queryString = require("query-string");
    const parsed = queryString.parse(props.location.search);
    ```

    You can also use `URLSearchParams` if you want something native:

    ```javascript
    const params = new URLSearchParams(props.location.search);
    const foo = params.get("name");
    ```

    You should use a _polyfill_ for IE11.

85. ### Why you get "Router may have only one child element" warning?

    You have to wrap your Route's in a `<Switch>` block because `<Switch>` is unique in that it renders a route exclusively.

    At first you need to add `Switch` to your imports:

    ```javascript
    import { Switch, Router, Route } from "react-router";
    ```

    Then define the routes within `<Switch>` block:

    ```jsx harmony
    <Router>
      <Switch>
        <Route {/* ... */} />
        <Route {/* ... */} />
      </Switch>
    </Router>
    ```

86. ### How to pass params to `history.push` method in React Router v4?

    While navigating you can pass props to the `history` object:

    ```javascript
    this.props.history.push({
      pathname: "/template",
      search: "?name=sudheer",
      state: { detail: response.data },
    });
    ```

    The `search` property is used to pass query params in `push()` method.

87. ### How to implement _default_ or _NotFound_ page?

    A `<Switch>` renders the first child `<Route>` that matches. A `<Route>` with no path always matches. So you just need to simply drop path attribute as below

    ```jsx harmony
    <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/user" component={User} />
      <Route component={NotFound} />
    </Switch>
    ```

88. ### How to get history on React Router v4?

    Below are the list of steps to get history object on React Router v4,

    1.  Create a module that exports a `history` object and import this module across the project.

        For example, create `history.js` file:

        ```javascript
        import { createBrowserHistory } from "history";

        export default createBrowserHistory({
          /* pass a configuration object here if needed */
        });
        ```

    2.  You should use the `<Router>` component instead of built-in routers. Import the above `history.js` inside `index.js` file:

        ```jsx harmony
        import { Router } from "react-router-dom";
        import history from "./history";
        import App from "./App";

        ReactDOM.render(
          <Router history={history}>
            <App />
          </Router>,
          holder
        );
        ```

    3.  You can also use push method of `history` object similar to built-in history object:

        ```javascript
        // some-other-file.js
        import history from "./history";

        history.push("/go-here");
        ```

89. ### How to perform automatic redirect after login?

    The `react-router` package provides `<Redirect>` component in React Router. Rendering a `<Redirect>` will navigate to a new location. Like server-side redirects, the new location will override the current location in the history stack.

    ```javascript
    import { Redirect } from "react-router";

    export default function Login {
        if (this.state.isLoggedIn === true) {
          return <Redirect to="/your/redirect/page" />;
        } else {
          return <div>{"Login Please"}</div>;
        }
    }
    ```

      <details><summary><b>See Class</b></summary>
      <p>

    ```jsx
    import React, { Component } from "react";
    import { Redirect } from "react-router";

    export default class LoginComponent extends Component {
      render() {
        if (this.state.isLoggedIn === true) {
          return <Redirect to="/your/redirect/page" />;
        } else {
          return <div>{"Login Please"}</div>;
        }
      }
    }
    ```

       </p>
       </details>

## React Internationalization

90. ### What is React Intl?

    The _React Intl_ library makes internationalization in React straightforward, with off-the-shelf components and an API that can handle everything from formatting strings, dates, and numbers, to pluralization. React Intl is part of _FormatJS_ which provides bindings to React via its components and API.

91. ### What are the main features of React Intl?

    Below are the main features of React Intl,

    1.  Display numbers with separators.
    2.  Display dates and times correctly.
    3.  Display dates relative to "now".
    4.  Pluralize labels in strings.
    5.  Support for 150+ languages.
    6.  Runs in the browser and Node.
    7.  Built on standards.

92. ### What are the two ways of formatting in React Intl?

    The library provides two ways to format strings, numbers, and dates:

    1.  **Using react components:**

        ```jsx harmony
        <FormattedMessage
          id={"account"}
          defaultMessage={"The amount is less than minimum balance."}
        />
        ```

    2.  **Using an API:**

        ```javascript
        const messages = defineMessages({
          accountMessage: {
            id: "account",
            defaultMessage: "The amount is less than minimum balance.",
          },
        });

        formatMessage(messages.accountMessage);
        ```

93. ### How to use `<FormattedMessage>` as placeholder using React Intl?

    The `<Formatted... />` components from `react-intl` return elements, not plain text, so they can't be used for placeholders, alt text, etc. In that case, you should use lower level API `formatMessage()`. You can inject the `intl` object into your component using `injectIntl()` higher-order component and then format the message using `formatMessage()` available on that object.

    ```jsx harmony
    import React from "react";
    import { injectIntl, intlShape } from "react-intl";

    const MyComponent = ({ intl }) => {
      const placeholder = intl.formatMessage({ id: "messageId" });
      return <input placeholder={placeholder} />;
    };

    MyComponent.propTypes = {
      intl: intlShape.isRequired,
    };

    export default injectIntl(MyComponent);
    ```

94. ### How to access current locale with React Intl?

    You can get the current locale in any component of your application using `injectIntl()`:

    ```jsx harmony
    import { injectIntl, intlShape } from "react-intl";

    const MyComponent = ({ intl }) => (
      <div>{`The current locale is ${intl.locale}`}</div>
    );

    MyComponent.propTypes = {
      intl: intlShape.isRequired,
    };

    export default injectIntl(MyComponent);
    ```

95. ### How to format date using React Intl?

    The `injectIntl()` higher-order component will give you access to the `formatDate()` method via the props in your component. The method is used internally by instances of `FormattedDate` and it returns the string representation of the formatted date.

    ```jsx harmony
    import { injectIntl, intlShape } from "react-intl";

    const stringDate = this.props.intl.formatDate(date, {
      year: "numeric",
      month: "numeric",
      day: "numeric",
    });

    const MyComponent = ({ intl }) => (
      <div>{`The formatted date is ${stringDate}`}</div>
    );

    MyComponent.propTypes = {
      intl: intlShape.isRequired,
    };

    export default injectIntl(MyComponent);
    ```

## React Testing

96. ### What is Shallow Renderer in React testing?

    _Shallow rendering_ is useful for writing unit test cases in React. It lets you render a component _one level deep_ and assert facts about what its render method returns, without worrying about the behavior of child components, which are not instantiated or rendered.

    For example, if you have the following component:

    ```javascript
    function MyComponent() {
      return (
        <div>
          <span className={"heading"}>{"Title"}</span>
          <span className={"description"}>{"Description"}</span>
        </div>
      );
    }
    ```

    Then you can assert as follows:

    ```jsx harmony
    import ShallowRenderer from "react-test-renderer/shallow";

    // in your test
    const renderer = new ShallowRenderer();
    renderer.render(<MyComponent />);

    const result = renderer.getRenderOutput();

    expect(result.type).toBe("div");
    expect(result.props.children).toEqual([
      <span className={"heading"}>{"Title"}</span>,
      <span className={"description"}>{"Description"}</span>,
    ]);
    ```

97. ### What is `TestRenderer` package in React?

    This package provides a renderer that can be used to render components to pure JavaScript objects, without depending on the DOM or a native mobile environment. This package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree) rendered by a ReactDOM or React Native without using a browser or `jsdom`.

    ```jsx harmony
    import TestRenderer from "react-test-renderer";

    const Link = ({ page, children }) => <a href={page}>{children}</a>;

    const testRenderer = TestRenderer.create(
      <Link page={"https://www.facebook.com/"}>{"Facebook"}</Link>
    );

    console.log(testRenderer.toJSON());
    // {
    //   type: 'a',
    //   props: { href: 'https://www.facebook.com/' },
    //   children: [ 'Facebook' ]
    // }
    ```

98. ### What is the purpose of ReactTestUtils package?

    _ReactTestUtils_ are provided in the `with-addons` package and allow you to perform actions against a simulated DOM for the purpose of unit testing.

99. ### What is Jest?

    _Jest_ is a JavaScript unit testing framework created by Facebook based on Jasmine and provides automated mock creation and a `jsdom` environment. It's often used for testing components.

100.  ### What are the advantages of Jest over Jasmine?

      There are couple of advantages compared to Jasmine:

      - Automatically finds tests to execute in your source code.
      - Automatically mocks dependencies when running your tests.
      - Allows you to test asynchronous code synchronously.
      - Runs your tests with a fake DOM implementation (via `jsdom`) so that your tests can be run on the command line.
      - Runs tests in parallel processes so that they finish sooner.

101.  ### Give a simple example of Jest test case

      Let's write a test for a function that adds two numbers in `sum.js` file:

      ```javascript
      const sum = (a, b) => a + b;

      export default sum;
      ```

      Create a file named `sum.test.js` which contains actual test:

      ```javascript
      import sum from "./sum";

      test("adds 1 + 2 to equal 3", () => {
        expect(sum(1, 2)).toBe(3);
      });
      ```

      And then add the following section to your `package.json`:

      ```json
      {
        "scripts": {
          "test": "jest"
        }
      }
      ```

      Finally, run `yarn test` or `npm test` and Jest will print a result:

      ```console
      $ yarn test
      PASS ./sum.test.js
      ✓ adds 1 + 2 to equal 3 (2ms)
      ```

## React Redux

102. ### What is flux?

     _Flux_ is an _application design paradigm_ used as a replacement for the more traditional MVC pattern. It is not a framework or a library but a new kind of architecture that complements React and the concept of Unidirectional Data Flow. Facebook uses this pattern internally when working with React.

     The workflow between dispatcher, stores and views components with distinct inputs and outputs as follows:

     ![flux](images/flux.png)

103. ### What is Redux?

     _Redux_ is a predictable state container for JavaScript apps based on the _Flux design pattern_. Redux can be used together with React, or with any other view library. It is tiny (about 2kB) and has no dependencies.

104. ### What are the core principles of Redux?

     Redux follows three fundamental principles:

     1. **Single source of truth:** The state of your whole application is stored in an object tree within a single store. The single state tree makes it easier to keep track of changes over time and debug or inspect the application.
     2. **State is read-only:** The only way to change the state is to emit an action, an object describing what happened. This ensures that neither the views nor the network callbacks will ever write directly to the state.
     3. **Changes are made with pure functions:** To specify how the state tree is transformed by actions, you write reducers. Reducers are just pure functions that take the previous state and an action as parameters, and return the next state.

105. ### What are the downsides of Redux compared to Flux?

     Instead of saying downsides we can say that there are few compromises of using Redux over Flux. Those are as follows:

     1. **You will need to learn to avoid mutations:** Flux is un-opinionated about mutating data, but Redux doesn't like mutations and many packages complementary to Redux assume you never mutate the state. You can enforce this with dev-only packages like `redux-immutable-state-invariant`, Immutable.js, or instructing your team to write non-mutating code.
     2. **You're going to have to carefully pick your packages:** While Flux explicitly doesn't try to solve problems such as undo/redo, persistence, or forms, Redux has extension points such as middleware and store enhancers, and it has spawned a rich ecosystem.
     3. **There is no nice Flow integration yet:** Flux currently lets you do very impressive static type checks which Redux doesn't support yet.

106. ### What is the difference between `mapStateToProps()` and `mapDispatchToProps()`?

     `mapStateToProps()` is a utility which helps your component get updated state (which is updated by some other components):

     ```javascript
     const mapStateToProps = (state) => {
       return {
         todos: getVisibleTodos(state.todos, state.visibilityFilter),
       };
     };
     ```

     `mapDispatchToProps()` is a utility which will help your component to fire an action event (dispatching action which may cause change of application state):

     ```javascript
     const mapDispatchToProps = (dispatch) => {
       return {
         onTodoClick: (id) => {
           dispatch(toggleTodo(id));
         },
       };
     };
     ```

     It is recommended to always use the “object shorthand” form for the `mapDispatchToProps`.

     Redux wraps it in another function that looks like (…args) => dispatch(onTodoClick(…args)), and pass that wrapper function as a prop to your component.

     ```javascript
     const mapDispatchToProps = {
       onTodoClick,
     };
     ```

107. ### Can I dispatch an action in reducer?

     Dispatching an action within a reducer is an **anti-pattern**. Your reducer should be _without side effects_, simply digesting the action payload and returning a new state object. Adding listeners and dispatching actions within the reducer can lead to chained actions and other side effects.

108. ### How to access Redux store outside a component?

     You just need to export the store from the module where it created with `createStore()`. Also, it shouldn't pollute the global window object.

     ```javascript
     store = createStore(myReducer);

     export default store;
     ```

109. ### What are the drawbacks of MVW pattern?

     1. DOM manipulation is very expensive which causes applications to behave slow and inefficient.
     2. Due to circular dependencies, a complicated model was created around models and views.
     3. Lot of data changes happens for collaborative applications(like Google Docs).
     4. No way to do undo (travel back in time) easily without adding so much extra code.

110. ### Are there any similarities between Redux and RxJS?

     These libraries are very different for very different purposes, but there are some vague similarities.

     Redux is a tool for managing state throughout the application. It is usually used as an architecture for UIs. Think of it as an alternative to (half of) Angular. RxJS is a reactive programming library. It is usually used as a tool to accomplish asynchronous tasks in JavaScript. Think of it as an alternative to Promises. Redux uses the Reactive paradigm because the Store is reactive. The Store observes actions from a distance, and changes itself. RxJS also uses the Reactive paradigm, but instead of being an architecture, it gives you basic building blocks, Observables, to accomplish this pattern.

111. ### How to reset state in Redux?

     You need to write a _root reducer_ in your application which delegate handling the action to the reducer generated by `combineReducers()`.

     For example, let us take `rootReducer()` to return the initial state after `USER_LOGOUT` action. As we know, reducers are supposed to return the initial state when they are called with `undefined` as the first argument, no matter the action.

     ```javascript
     const appReducer = combineReducers({
       /* your app's top-level reducers */
     });

     const rootReducer = (state, action) => {
       if (action.type === "USER_LOGOUT") {
         state = undefined;
       }

       return appReducer(state, action);
     };
     ```

     In case of using `redux-persist`, you may also need to clean your storage. `redux-persist` keeps a copy of your state in a storage engine. First, you need to import the appropriate storage engine and then, to parse the state before setting it to undefined and clean each storage state key.

     ```javascript
     const appReducer = combineReducers({
       /* your app's top-level reducers */
     });

     const rootReducer = (state, action) => {
       if (action.type === "USER_LOGOUT") {
         Object.keys(state).forEach((key) => {
           storage.removeItem(`persist:${key}`);
         });

         state = undefined;
       }

       return appReducer(state, action);
     };
     ```

112. ### What is the difference between React context and React Redux?

     You can use **Context** in your application directly and is going to be great for passing down data to deeply nested components which what it was designed for.

     Whereas **Redux** is much more powerful and provides a large number of features that the Context API doesn't provide. Also, React Redux uses context internally but it doesn't expose this fact in the public API.

113. ### Why are Redux state functions called reducers?

     Reducers always return the accumulation of the state (based on all previous and current actions). Therefore, they act as a reducer of state. Each time a Redux reducer is called, the state and action are passed as parameters. This state is then reduced (or accumulated) based on the action, and then the next state is returned. You could _reduce_ a collection of actions and an initial state (of the store) on which to perform these actions to get the resulting final state.

114. ### How to make AJAX request in Redux?

     You can use `redux-thunk` middleware which allows you to define async actions.

     Let's take an example of fetching specific account as an AJAX call using _fetch API_:

     ```javascript
     export function fetchAccount(id) {
       return (dispatch) => {
         dispatch(setLoadingAccountState()); // Show a loading spinner
         fetch(`/account/${id}`, (response) => {
           dispatch(doneFetchingAccount()); // Hide loading spinner
           if (response.status === 200) {
             dispatch(setAccount(response.json)); // Use a normal function to set the received state
           } else {
             dispatch(someError);
           }
         });
       };
     }

     function setAccount(data) {
       return { type: "SET_Account", data: data };
     }
     ```

115. ### Should I keep all component's state in Redux store?

     Keep your data in the Redux store, and the UI related state internally in the component.

116. ### What is the proper way to access Redux store?

     The best way to access your store in a component is to use the `connect()` function, that creates a new component that wraps around your existing one. This pattern is called _Higher-Order Components_, and is generally the preferred way of extending a component's functionality in React. This allows you to map state and action creators to your component, and have them passed in automatically as your store updates.

     Let's take an example of `<FilterLink>` component using connect:

     ```javascript
     import { connect } from "react-redux";
     import { setVisibilityFilter } from "../actions";
     import Link from "../components/Link";

     const mapStateToProps = (state, ownProps) => ({
       active: ownProps.filter === state.visibilityFilter,
     });

     const mapDispatchToProps = (dispatch, ownProps) => ({
       onClick: () => dispatch(setVisibilityFilter(ownProps.filter)),
     });

     const FilterLink = connect(mapStateToProps, mapDispatchToProps)(Link);

     export default FilterLink;
     ```

     Due to it having quite a few performance optimizations and generally being less likely to cause bugs, the Redux developers almost always recommend using `connect()` over accessing the store directly (using context API).

     ```javascript
     function MyComponent {
       someMethod() {
         doSomethingWith(this.context.store);
       }
     }
     ```

117. ### What is the difference between component and container in React Redux?

     **Component** is a class or function component that describes the presentational part of your application.

     **Container** is an informal term for a component that is connected to a Redux store. Containers _subscribe_ to Redux state updates and _dispatch_ actions, and they usually don't render DOM elements; they delegate rendering to presentational child components.

118. ### What is the purpose of the constants in Redux?

     Constants allows you to easily find all usages of that specific functionality across the project when you use an IDE. It also prevents you from introducing silly bugs caused by typos – in which case, you will get a `ReferenceError` immediately.

     Normally we will save them in a single file (`constants.js` or `actionTypes.js`).

     ```javascript
     export const ADD_TODO = "ADD_TODO";
     export const DELETE_TODO = "DELETE_TODO";
     export const EDIT_TODO = "EDIT_TODO";
     export const COMPLETE_TODO = "COMPLETE_TODO";
     export const COMPLETE_ALL = "COMPLETE_ALL";
     export const CLEAR_COMPLETED = "CLEAR_COMPLETED";
     ```

     In Redux, you use them in two places:

     1. **During action creation:**

        Let's take `actions.js`:

        ```javascript
        import { ADD_TODO } from "./actionTypes";

        export function addTodo(text) {
          return { type: ADD_TODO, text };
        }
        ```

     2. **In reducers:**

        Let's create `reducer.js`:

        ```javascript
        import { ADD_TODO } from "./actionTypes";

        export default (state = [], action) => {
          switch (action.type) {
            case ADD_TODO:
              return [
                ...state,
                {
                  text: action.text,
                  completed: false,
                },
              ];
            default:
              return state;
          }
        };
        ```

119. ### What are the different ways to write `mapDispatchToProps()`?

     There are a few ways of binding _action creators_ to `dispatch()` in `mapDispatchToProps()`.

     Below are the possible options:

     ```javascript
     const mapDispatchToProps = (dispatch) => ({
       action: () => dispatch(action()),
     });
     ```

     ```javascript
     const mapDispatchToProps = (dispatch) => ({
       action: bindActionCreators(action, dispatch),
     });
     ```

     ```javascript
     const mapDispatchToProps = { action };
     ```

     The third option is just a shorthand for the first one.

120. ### What is the use of the `ownProps` parameter in `mapStateToProps()` and `mapDispatchToProps()`?

     If the `ownProps` parameter is specified, React Redux will pass the props that were passed to the component into your _connect_ functions. So, if you use a connected component:

     ```jsx harmony
     import ConnectedComponent from "./containers/ConnectedComponent";

     <ConnectedComponent user={"john"} />;
     ```

     The `ownProps` inside your `mapStateToProps()` and `mapDispatchToProps()` functions will be an object:

     ```javascript
     {
       user: "john";
     }
     ```

     You can use this object to decide what to return from those functions.

121. ### How to structure Redux top level directories?

     Most of the applications has several top-level directories as below:

     1. **Components**: Used for _dumb_ components unaware of Redux.
     2. **Containers**: Used for _smart_ components connected to Redux.
     3. **Actions**: Used for all action creators, where file names correspond to part of the app.
     4. **Reducers**: Used for all reducers, where files name correspond to state key.
     5. **Store**: Used for store initialization.

     This structure works well for small and medium size apps.

122. ### What is redux-saga?

     `redux-saga` is a library that aims to make side effects (asynchronous things like data fetching and impure things like accessing the browser cache) in React/Redux applications easier and better.

     It is available in NPM:

     ```console
     $ npm install --save redux-saga
     ```

123. ### What is the mental model of redux-saga?

     _Saga_ is like a separate thread in your application, that's solely responsible for side effects. `redux-saga` is a redux _middleware_, which means this thread can be started, paused and cancelled from the main application with normal Redux actions, it has access to the full Redux application state and it can dispatch Redux actions as well.

124. ### What are the differences between `call()` and `put()` in redux-saga?

     Both `call()` and `put()` are effect creator functions. `call()` function is used to create effect description, which instructs middleware to call the promise. `put()` function creates an effect, which instructs middleware to dispatch an action to the store.

     Let's take example of how these effects work for fetching particular user data.

     ```javascript
     function* fetchUserSaga(action) {
       // `call` function accepts rest arguments, which will be passed to `api.fetchUser` function.
       // Instructing middleware to call promise, it resolved value will be assigned to `userData` variable
       const userData = yield call(api.fetchUser, action.userId);

       // Instructing middleware to dispatch corresponding action.
       yield put({
         type: "FETCH_USER_SUCCESS",
         userData,
       });
     }
     ```

125. ### What is Redux Thunk?

     _Redux Thunk_ middleware allows you to write action creators that return a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met. The inner function receives the store methods `dispatch()` and `getState()` as parameters.

126. ### What are the differences between `redux-saga` and `redux-thunk`?

     Both _Redux Thunk_ and _Redux Saga_ take care of dealing with side effects. In most of the scenarios, Thunk uses _Promises_ to deal with them, whereas Saga uses _Generators_. Thunk is simple to use and Promises are familiar to many developers, Sagas/Generators are more powerful but you will need to learn them. But both middleware can coexist, so you can start with Thunks and introduce Sagas when/if you need them.

127. ### What is Redux DevTools?

     _Redux DevTools_ is a live-editing time travel environment for Redux with hot reloading, action replay, and customizable UI. If you don't want to bother with installing Redux DevTools and integrating it into your project, consider using Redux DevTools Extension for Chrome and Firefox.

128. ### What are the features of Redux DevTools?

     Some of the main features of Redux DevTools are below,

     1. Lets you inspect every state and action payload.
     2. Lets you go back in time by _cancelling_ actions.
     3. If you change the reducer code, each _staged_ action will be re-evaluated.
     4. If the reducers throw, you will see during which action this happened, and what the error was.
     5. With `persistState()` store enhancer, you can persist debug sessions across page reloads.

129. ### What are Redux selectors and why use them?

     _Selectors_ are functions that take Redux state as an argument and return some data to pass to the component.

     For example, to get user details from the state:

     ```javascript
     const getUserData = (state) => state.user.data;
     ```

     These selectors have two main benefits,

     1. The selector can compute derived data, allowing Redux to store the minimal possible state
     2. The selector is not recomputed unless one of its arguments changes

130. ### What is Redux Form?

     _Redux Form_ works with React and Redux to enable a form in React to use Redux to store all of its state. Redux Form can be used with raw HTML5 inputs, but it also works very well with common UI frameworks like Material UI, React Widgets and React Bootstrap.

131. ### What are the main features of Redux Form?

     Some of the main features of Redux Form are:

     1. Field values persistence via Redux store.
     2. Validation (sync/async) and submission.
     3. Formatting, parsing and normalization of field values.

132. ### How to add multiple middlewares to Redux?

     You can use `applyMiddleware()`.

     For example, you can add `redux-thunk` and `logger` passing them as arguments to `applyMiddleware()`:

     ```javascript
     import { createStore, applyMiddleware } from "redux";
     const createStoreWithMiddleware = applyMiddleware(
       ReduxThunk,
       logger
     )(createStore);
     ```

133. ### How to set initial state in Redux?

     You need to pass initial state as second argument to createStore:

     ```javascript
     const rootReducer = combineReducers({
       todos: todos,
       visibilityFilter: visibilityFilter,
     });

     const initialState = {
       todos: [{ id: 123, name: "example", completed: false }],
     };

     const store = createStore(rootReducer, initialState);
     ```

134. ### How Relay is different from Redux?

     Relay is similar to Redux in that they both use a single store. The main difference is that relay only manages state originated from the server, and all access to the state is used via _GraphQL_ queries (for reading data) and mutations (for changing data). Relay caches the data for you and optimizes data fetching for you, by fetching only changed data and nothing more.

135. ### What is an action in Redux?

     _Actions_ are plain JavaScript objects or payloads of information that send data from your application to your store. They are the only source of information for the store. Actions must have a type property that indicates the type of action being performed.

     For example, let's take an action which represents adding a new todo item:

     ```
     {
       type: ADD_TODO,
       text: 'Add todo item'
     }
     ```

## React Native

136. ### What is the difference between React Native and React?

     **React** is a JavaScript library, supporting both front end web and being run on the server, for building user interfaces and web applications.

     **React Native** is a mobile framework that compiles to native app components, allowing you to build native mobile applications (iOS, Android, and Windows) in JavaScript that allows you to use React to build your components, and implements React under the hood.

137. ### How to test React Native apps?

     React Native can be tested only in mobile simulators like iOS and Android. You can run the app in your mobile using expo app (https://expo.io) Where it syncs using QR code, your mobile and computer should be in same wireless network.

138. ### How to do logging in React Native?

     You can use `console.log`, `console.warn`, etc. As of React Native v0.29 you can simply run the following to see logs in the console:

     ```
     $ react-native log-ios
     $ react-native log-android
     ```

139. ### How to debug your React Native?

     Follow the below steps to debug React Native app:

     1. Run your application in the iOS simulator.
     2. Press `Command + D` and a webpage should open up at `http://localhost:8081/debugger-ui`.
     3. Enable _Pause On Caught Exceptions_ for a better debugging experience.
     4. Press `Command + Option + I` to open the Chrome Developer tools, or open it via `View` -> `Developer` -> `Developer Tools`.
     5. You should now be able to debug as you normally would.

## React supported libraries & Integration

140. ### What is reselect and how it works?

     _Reselect_ is a **selector library** (for Redux) which uses _memoization_ concept. It was originally written to compute derived data from Redux-like applications state, but it can't be tied to any architecture or library.

     Reselect keeps a copy of the last inputs/outputs of the last call, and recomputes the result only if one of the inputs changes. If the same inputs are provided twice in a row, Reselect returns the cached output. It's memoization and cache are fully customizable.

141. ### What is Flow?

     _Flow_ is a _static type checker_ designed to find type errors in JavaScript. Flow types can express much more fine-grained distinctions than traditional type systems. For example, Flow helps you catch errors involving `null`, unlike most type systems.

142. ### What is the difference between Flow and PropTypes?

     Flow is a _static analysis tool_ (static checker) which uses a superset of the language, allowing you to add type annotations to all of your code and catch an entire class of bugs at compile time.

     PropTypes is a _basic type checker_ (runtime checker) which has been patched onto React. It can't check anything other than the types of the props being passed to a given component. If you want more flexible typechecking for your entire project Flow/TypeScript are appropriate choices.

143. ### How to use Font Awesome icons in React?

     The below steps followed to include Font Awesome in React:

     1. Install `font-awesome`:

        ```console
        $ npm install --save font-awesome
        ```

     2. Import `font-awesome` in your `index.js` file:

        ```javascript
        import "font-awesome/css/font-awesome.min.css";
        ```

     3. Add Font Awesome classes in `className`:

        ```javascript
        function MyComponent {
          return <div><i className={'fa fa-spinner'} /></div>
        }
        ```

144. ### What is React Dev Tools?

     _React Developer Tools_ let you inspect the component hierarchy, including component props and state. It exists both as a browser extension (for Chrome and Firefox), and as a standalone app (works with other environments including Safari, IE, and React Native).

     The official extensions available for different browsers or environments.

     1. **Chrome extension**
     2. **Firefox extension**
     3. **Standalone app** (Safari, React Native, etc)

145. ### Why is DevTools not loading in Chrome for local files?

     If you opened a local HTML file in your browser (`file://...`) then you must first open _Chrome Extensions_ and check `Allow access to file URLs`.

146. ### How to use Polymer in React?

     You need to follow below steps to use Polymer in React,

     1. Create a Polymer element:

        ```jsx harmony
        <link
          rel="import"
          href="../../bower_components/polymer/polymer.html"
        />;
        Polymer({
          is: "calendar-element",
          ready: function () {
            this.textContent = "I am a calendar";
          },
        });
        ```

     2. Create the Polymer component HTML tag by importing it in a HTML document, e.g. import it in the `index.html` of your React application:

        ```html
        <link
          rel="import"
          href="./src/polymer-components/calendar-element.html"
        />
        ```

     3. Use that element in the JSX file:

        ```javascript
        export default function MyComponent {
          return <calendar-element />;
        }
        ```

147. ### What are the advantages of React over Vue.js?

     React has the following advantages over Vue.js:

     1. Gives more flexibility in large apps developing.
     2. Easier to test.
     3. Suitable for mobile apps creating.
     4. More information and solutions available.

**Note:** The above list of advantages are purely opinionated and it vary based on the professional experience. But they are helpful as base parameters.

148. ### What is the difference between React and Angular?

     Let's see the difference between React and Angular in a table format.

     | React                                                                                       | Angular                                                                                                                            |
     | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
     | React is a library and has only the View layer                                              | Angular is a framework and has complete MVC functionality                                                                          |
     | React handles rendering on the server side                                                  | AngularJS renders only on the client side but Angular 2 and above renders on the server side                                       |
     | React uses JSX that looks like HTML in JS which can be confusing                            | Angular follows the template approach for HTML, which makes code shorter and easy to understand                                    |
     | React Native, which is a React type to build mobile applications are faster and more stable | Ionic, Angular's mobile native app is relatively less stable and slower                                                            |
     | In React, data flows only in one way and hence debugging is easy                            | In Angular, data flows both way i.e it has two-way data binding between children and parent and hence debugging is often difficult |

**Note:** The above list of differences are purely opinionated and it vary based on the professional experience. But they are helpful as base parameters.

149. ### Why React tab is not showing up in DevTools?

     When the page loads, _React DevTools_ sets a global named `__REACT_DEVTOOLS_GLOBAL_HOOK__`, then React communicates with that hook during initialization. If the website is not using React or if React fails to communicate with DevTools then it won't show up the tab.

150. ### What are Styled Components?

     `styled-components` is a JavaScript library for styling React applications. It removes the mapping between styles and components, and lets you write actual CSS augmented with JavaScript.

151. ### Give an example of Styled Components?

     Lets create `<Title>` and `<Wrapper>` components with specific styles for each.

     ```javascript
     import React from "react";
     import styled from "styled-components";

     // Create a <Title> component that renders an <h1> which is centered, red and sized at 1.5em
     const Title = styled.h1`
       font-size: 1.5em;
       text-align: center;
       color: palevioletred;
     `;

     // Create a <Wrapper> component that renders a <section> with some padding and a papayawhip background
     const Wrapper = styled.section`
       padding: 4em;
       background: papayawhip;
     `;
     ```

     These two variables, `Title` and `Wrapper`, are now components that you can render just like any other react component.

     ```jsx harmony
     <Wrapper>
       <Title>{"Lets start first styled component!"}</Title>
     </Wrapper>
     ```

152. ### What is Relay?

     Relay is a JavaScript framework for providing a data layer and client-server communication to web applications using the React view layer.

## Miscellaneous

153. ### What are the main features of Reselect library?

     Let's see the main features of Reselect library,

     1. Selectors can compute derived data, allowing Redux to store the minimal possible state.
     2. Selectors are efficient. A selector is not recomputed unless one of its arguments changes.
     3. Selectors are composable. They can be used as input to other selectors.

154. #### Give an example of Reselect usage?

     Let's take calculations and different amounts of a shipment order with the simplified usage of Reselect:

     ```javascript
     import { createSelector } from "reselect";

     const shopItemsSelector = (state) => state.shop.items;
     const taxPercentSelector = (state) => state.shop.taxPercent;

     const subtotalSelector = createSelector(shopItemsSelector, (items) =>
       items.reduce((acc, item) => acc + item.value, 0)
     );

     const taxSelector = createSelector(
       subtotalSelector,
       taxPercentSelector,
       (subtotal, taxPercent) => subtotal * (taxPercent / 100)
     );

     export const totalSelector = createSelector(
       subtotalSelector,
       taxSelector,
       (subtotal, tax) => ({ total: subtotal + tax })
     );

     let exampleState = {
       shop: {
         taxPercent: 8,
         items: [
           { name: "apple", value: 1.2 },
           { name: "orange", value: 0.95 },
         ],
       },
     };

     console.log(subtotalSelector(exampleState)); // 2.15
     console.log(taxSelector(exampleState)); // 0.172
     console.log(totalSelector(exampleState)); // { total: 2.322 }
     ```

155. ### Can Redux only be used with React?

     Redux can be used as a data store for any UI layer. The most common usage is with React and React Native, but there are bindings available for Angular, Angular 2, Vue, Mithril, and more. Redux simply provides a subscription mechanism which can be used by any other code.

156. ### Do you need to have a particular build tool to use Redux?

     Redux is originally written in ES6 and transpiled for production into ES5 with Webpack and Babel. You should be able to use it regardless of your JavaScript build process. Redux also offers a UMD build that can be used directly without any build process at all.

157. ### How Redux Form `initialValues` get updated from state?

     You need to add `enableReinitialize : true` setting.

     ```javascript
     const InitializeFromStateForm = reduxForm({
       form: "initializeFromState",
       enableReinitialize: true,
     })(UserEdit);
     ```

     If your `initialValues` prop gets updated, your form will update too.

158. ### How React PropTypes allow different types for one prop?

     You can use `oneOfType()` method of `PropTypes`.

     For example, the height property can be defined with either `string` or `number` type as below:

     ```javascript
     Component.propTypes = {
       size: PropTypes.oneOfType([PropTypes.string, PropTypes.number]),
     };
     ```

159. ### Can I import an SVG file as react component?

     You can import SVG directly as component instead of loading it as a file. This feature is available with `react-scripts@2.0.0` and higher.

     ```jsx harmony
     import { ReactComponent as Logo } from "./logo.svg";

     const App = () => (
       <div>
         {/* Logo is an actual react component */}
         <Logo />
       </div>
     );
     ```

     **Note**: Don't forget about the curly braces in the import.

160. ### What is render hijacking in react?

     The concept of render hijacking is the ability to control what a component will output from another component. It means that you decorate your component by wrapping it into a Higher-Order component. By wrapping, you can inject additional props or make other changes, which can cause changing logic of rendering. It does not actually enable hijacking, but by using HOC you make your component behave differently.

161. ### How to pass numbers to React component?

     We can pass `numbers` as `props` to React component using curly braces `{}` where as `strings` in double quotes `""` or single quotes `''`

     ```jsx
     import React from "react";

     const ChildComponent = ({ name, age }) => {
       return (
         <>
           My Name is {name} and Age is {age}
         </>
       );
     };

     const ParentComponent = () => {
       return (
         <>
           <ChildComponent name="Chetan" age={30} />
         </>
       );
     };

     export default ParentComponent;
     ```

162. ### Do I need to keep all my state into Redux? Should I ever use react internal state?

     It is up to the developer's decision, i.e., it is developer's job to determine what kinds of state make up your application, and where each piece of state should live. Some users prefer to keep every single piece of data in Redux, to maintain a fully serializable and controlled version of their application at all times. Others prefer to keep non-critical or UI state, such as “is this dropdown currently open”, inside a component's internal state.

     Below are the rules of thumb to determine what kind of data should be put into Redux

     1. Do other parts of the application care about this data?
     2. Do you need to be able to create further derived data based on this original data?
     3. Is the same data being used to drive multiple components?
     4. Is there value to you in being able to restore this state to a given point in time (ie, time travel debugging)?
     5. Do you want to cache the data (i.e, use what's in state if it's already there instead of re-requesting it)?

163. ### What is the purpose of registerServiceWorker in React?

     React creates a service worker for you without any configuration by default. The service worker is a web API that helps you cache your assets and other files so that when the user is offline or on a slow network, he/she can still see results on the screen, as such, it helps you build a better user experience, that's what you should know about service worker for now. It's all about adding offline capabilities to your site.

     ```jsx
     import React from "react";
     import ReactDOM from "react-dom";
     import App from "./App";
     import registerServiceWorker from "./registerServiceWorker";

     ReactDOM.render(<App />, document.getElementById("root"));
     registerServiceWorker();
     ```

164. ### What is React memo function?

     Class components can be restricted from re-rendering when their input props are the same using **PureComponent or shouldComponentUpdate**. Now you can do the same with function components by wrapping them in **React.memo**.

     ```jsx
     const MyComponent = React.memo(function MyComponent(props) {
       /* only rerenders if props change */
     });
     ```

165. ### What is React lazy function?

     The `React.lazy` function lets you render a dynamic import as a regular component. It will automatically load the bundle containing the `OtherComponent` when the component gets rendered. This must return a Promise which resolves to a module with a default export containing a React component.

     ```jsx
     const OtherComponent = React.lazy(() => import("./OtherComponent"));

     function MyComponent() {
       return (
         <div>
           <OtherComponent />
         </div>
       );
     }
     ```

     **Note:**
     `React.lazy` and `Suspense` is not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we still recommend React Loadable.

166. ### How to prevent unnecessary updates using setState?

     You can compare the current value of the state with an existing state value and decide whether to rerender the page or not. If the values are the same then you need to return **null** to stop re-rendering otherwise return the latest state value.

     For example, the user profile information is conditionally rendered as follows,

     ```jsx
     getUserProfile = (user) => {
       const latestAddress = user.address;
       this.setState((state) => {
         if (state.address === latestAddress) {
           return null;
         } else {
           return { title: latestAddress };
         }
       });
     };
     ```

167. ### How do you render Array, Strings and Numbers in React 16 Version?

     **Arrays**: Unlike older releases, you don't need to make sure **render** method return a single element in React16. You are able to return multiple sibling elements without a wrapping element by returning an array.

     For example, let us take the below list of developers,

     ```jsx
     const ReactJSDevs = () => {
       return [
         <li key="1">John</li>,
         <li key="2">Jackie</li>,
         <li key="3">Jordan</li>,
       ];
     };
     ```

     You can also merge this array of items in another array component.

     ```jsx
     const JSDevs = () => {
       return (
         <ul>
           <li>Brad</li>
           <li>Brodge</li>
           <ReactJSDevs />
           <li>Brandon</li>
         </ul>
       );
     };
     ```

     **Strings and Numbers:** You can also return string and number type from the render method.

     ```jsx
     render() {
      return 'Welcome to ReactJS questions';
     }
     // Number
     render() {
      return 2018;
     }
     ```

168. ### What are hooks?

     Hooks is a special JavaScript function that allows you use state and other React features without writing a class. This pattern has been introduced as a new feature in React 16.8 and helped to isolate the stateful logic from the components.

     Let's see an example of useState hook:

     ```jsx
     import { useState } from "react";

     function Example() {
       // Declare a new state variable, which we'll call "count"
       const [count, setCount] = useState(0);

       return (
         <>
           <p>You clicked {count} times</p>
           <button onClick={() => setCount(count + 1)}>Click me</button>
         </>
       );
     }
     ```

     **Note:** Hooks can be used inside an existing function component without rewriting the component.

169. ### What rules need to be followed for hooks?

     You need to follow two rules in order to use hooks,

     1. **Call Hooks only at the top level of your react functions:** You should always use hooks at the top level of react function before any early returns. i.e, You shouldn’t call Hooks inside loops, conditions, or nested functions. This will ensure that Hooks are called in the same order each time a component renders and it preserves the state of Hooks between multiple re-renders due to useState and useEffect calls.
     2. **Call Hooks from React Functions only:** You shouldn’t call Hooks from regular JavaScript functions or class components. Instead, you should call them from either function components or custom hooks.

170. ### How to ensure hooks followed the rules in your project?

     React team released an ESLint plugin called **eslint-plugin-react-hooks** that enforces Hook's two rules. It is part of Hooks API. You can add this plugin to your project using the below command,

     ```javascript
     npm install eslint-plugin-react-hooks --save-dev
     ```

     And apply the below config in your ESLint config file,

     ```javascript
     // Your ESLint configuration
     {
       "plugins": [
         // ...
         "react-hooks"
       ],
       "rules": {
         // ...
         "react-hooks/rules-of-hooks": "error"
       }
     }
     ```

     The recommended `eslint-config-react-app` preset already includes the hooks rules of this plugin.
     For example, the linter enforce proper naming convention for hooks. If you rename your custom hooks which as prefix "use" to something else then linter won't allow you to call built-in hooks such as useState, useEffect etc inside of your custom hook anymore.

     **Note:** This plugin is intended to use in Create React App by default.

171. ### What are the differences between Flux and Redux?

     Below are the major differences between Flux and Redux

     | Flux                                           | Redux                                      |
     | ---------------------------------------------- | ------------------------------------------ |
     | State is mutable                               | State is immutable                         |
     | The Store contains both state and change logic | The Store and change logic are separate    |
     | There are multiple stores exist                | There is only one store exist              |
     | All the stores are disconnected and flat       | Single store with hierarchical reducers    |
     | It has a singleton dispatcher                  | There is no concept of dispatcher          |
     | React components subscribe to the store        | Container components uses connect function |

172. ### What are the benefits of React Router V4?

     Below are the main benefits of React Router V4 module,

     1. In React Router v4(version 4), the API is completely about components. A router can be visualized as a single component(`<BrowserRouter>`) which wraps specific child router components(`<Route>`).
     2. You don't need to manually set history. The router module will take care history by wrapping routes with `<BrowserRouter>` component.
     3. The application size is reduced by adding only the specific router module(Web, core, or native)

173. ### Can you describe about componentDidCatch lifecycle method signature?

     The **componentDidCatch** lifecycle method is invoked after an error has been thrown by a descendant component. The method receives two parameters,

     1. error: - The error object which was thrown
     2. info: - An object with a componentStack key contains the information about which component threw the error.

     The method structure would be as follows

     ```javascript
     componentDidCatch(error, info);
     ```

174. ### In which scenarios do error boundaries not catch errors?

     Below are the cases in which error boundaries don't work,

     1. Inside Event handlers
     2. Asynchronous code using **setTimeout or requestAnimationFrame** callbacks
     3. During Server side rendering
     4. When errors thrown in the error boundary code itself

175. ### What is the behavior of uncaught errors in react 16?

     In React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree. The reason behind this decision is that it is worse to leave corrupted UI in place than to completely remove it. For example, it is worse for a payments app to display a wrong amount than to render nothing.

176. ### What is the proper placement for error boundaries?

     The granularity of error boundaries usage is up to the developer based on project needs. You can follow either of these approaches,

     1. You can wrap top-level route components to display a generic error message for the entire application.
     2. You can also wrap individual components in an error boundary to protect them from crashing the rest of the application.

177. ### What is the benefit of component stack trace from error boundary?

     Apart from error messages and javascript stack, React16 will display the component stack trace with file names and line numbers using error boundary concept.

     For example, BuggyCounter component displays the component stack trace as below,

     ![stacktrace](images/error_boundary.png)

178. ### What are default props?

     The _defaultProps_ can be defined as a property on the component to set the default values for the props. These default props are used when props not supplied(i.e., undefined props), but not for `null` or `0` as props. That means, If you provide null value then it remains null value. It's the same behavior with 0 as well.

     For example, let us create color default prop for the button component,

     ```javascript
     function MyButton {
       // ...
     }

     MyButton.defaultProps = {
       color: "red",
     };
     ```

     If `props.color` is not provided then it will set the default value to 'red'. i.e, Whenever you try to access the color prop it uses the default value

     ```javascript
     function MyButton() {
       return <MyButton />; // props.color will contain red value
     }
     ```

179. ### What is the purpose of displayName class property?

     The displayName string is used in debugging messages. Usually, you don’t need to set it explicitly because it’s inferred from the name of the function or class that defines the component. You might want to set it explicitly if you want to display a different name for debugging purposes or when you create a higher-order component.

     For example, To ease debugging, choose a display name that communicates that it’s the result of a withSubscription HOC.

     ```javascript
     function withSubscription(WrappedComponent) {
       class WithSubscription extends React.Component {
         /* ... */
       }
       WithSubscription.displayName = `WithSubscription(${getDisplayName(
         WrappedComponent
       )})`;
       return WithSubscription;
     }
     function getDisplayName(WrappedComponent) {
       return (
         WrappedComponent.displayName || WrappedComponent.name || "Component"
       );
     }
     ```

180. ### What is the browser support for react applications?

     React supports all popular browsers, including Internet Explorer 9 and above, although some polyfills are required for older browsers such as IE 9 and IE 10. If you use **es5-shim and es5-sham** polyfill then it even support old browsers that doesn't support ES5 methods.

181. ### What is code-splitting?

     Code-Splitting is a feature supported by bundlers like Webpack and Browserify which can create multiple bundles that can be dynamically loaded at runtime. The react project supports code splitting via dynamic import() feature.

     For example, in the below code snippets, it will make moduleA.js and all its unique dependencies as a separate chunk that only loads after the user clicks the 'Load' button.

     **moduleA.js**

     ```javascript
     const moduleA = "Hello";

     export { moduleA };
     ```

     **App.js**

     ```javascript
     export default function App {
       function handleClick() {
         import("./moduleA")
           .then(({ moduleA }) => {
             // Use moduleA
           })
           .catch((err) => {
             // Handle failure
           });
       };

      return (
        <div>
          <button onClick={this.handleClick}>Load</button>
        </div>
      );
     }
     ```

  <details><summary><b>See Class</b></summary>
    <p>

```javascript
import React, { Component } from "react";

class App extends Component {
  handleClick = () => {
    import("./moduleA")
      .then(({ moduleA }) => {
        // Use moduleA
      })
      .catch((err) => {
        // Handle failure
      });
  };

  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Load</button>
      </div>
    );
  }
}

export default App;
```

  </p>
</details>

182. ### What are Keyed Fragments?

     The Fragments declared with the explicit <React.Fragment> syntax may have keys. The general use case is mapping a collection to an array of fragments as below,

     ```javascript
     function Glossary(props) {
       return (
         <dl>
           {props.items.map((item) => (
             // Without the `key`, React will fire a key warning
             <React.Fragment key={item.id}>
               <dt>{item.term}</dt>
               <dd>{item.description}</dd>
             </React.Fragment>
           ))}
         </dl>
       );
     }
     ```

     **Note:** key is the only attribute that can be passed to Fragment. In the future, there might be a support for additional attributes, such as event handlers.

183. ### Does React support all HTML attributes?

     As of React 16, both standard or custom DOM attributes are fully supported. Since React components often take both custom and DOM-related props, React uses the camelCase convention just like the DOM APIs.

     Let us take few props with respect to standard HTML attributes,

     ```javascript
     <div tabIndex="-1" />      // Just like node.tabIndex DOM API
     <div className="Button" /> // Just like node.className DOM API
     <input readOnly={true} />  // Just like node.readOnly DOM API
     ```

     These props work similarly to the corresponding HTML attributes, with the exception of the special cases. It also support all SVG attributes.

184. ### When component props defaults to true?

     If you pass no value for a prop, it defaults to true. This behavior is available so that it matches the behavior of HTML.

     For example, below expressions are equivalent,

     ```javascript
     <MyInput autocomplete />

     <MyInput autocomplete={true} />
     ```

     **Note:** It is not recommended to use this approach because it can be confused with the ES6 object shorthand (example, `{name}` which is short for `{name: name}`)

185. ### What is NextJS and major features of it?

     Next.js is a popular and lightweight framework for static and server‑rendered applications built with React. It also provides styling and routing solutions. Below are the major features provided by NextJS,

     1. Server-rendered by default
     2. Automatic code splitting for faster page loads
     3. Simple client-side routing (page based)
     4. Webpack-based dev environment which supports (HMR)
     5. Able to implement with Express or any other Node.js HTTP server
     6. Customizable with your own Babel and Webpack configurations

186. ### How do you pass an event handler to a component?

     You can pass event handlers and other functions as props to child components. The functions can be passed to child component as below,

     ```jsx
     function Button({ onClick }) {
       return <button onClick={onClick}>Download</button>;
     }

     export default function downloadExcel() {
       function handleClick() {
         alert("Downloaded");
       }

       return <Button onClick={handleClick}></Button>;
     }
     ```

187. ### How to prevent a function from being called multiple times?

     If you use an event handler such as **onClick or onScroll** and want to prevent the callback from being fired too quickly, then you can limit the rate at which callback is executed. This can be achieved in the below possible ways,

     1. **Throttling:** Changes based on a time based frequency. For example, it can be used using \_.throttle lodash function
     2. **Debouncing:** Publish changes after a period of inactivity. For example, it can be used using \_.debounce lodash function
     3. **RequestAnimationFrame throttling:** Changes based on requestAnimationFrame. For example, it can be used using raf-schd lodash function

188. ### How JSX prevents Injection Attacks?

     React DOM escapes any values embedded in JSX before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application. Everything is converted to a string before being rendered.

     For example, you can embed user input as below,

     ```javascript
     const name = response.potentiallyMaliciousInput;
     const element = <h1>{name}</h1>;
     ```

     This way you can prevent XSS(Cross-site-scripting) attacks in the application.

189. ### How do you update rendered elements?

     You can update UI(represented by rendered element) by passing the newly created element to ReactDOM's render method.

     For example, lets take a ticking clock example, where it updates the time by calling render method multiple times,

     ```javascript
     function tick() {
       const element = (
         <div>
           <h1>Hello, world!</h1>
           <h2>It is {new Date().toLocaleTimeString()}.</h2>
         </div>
       );
       ReactDOM.render(element, document.getElementById("root"));
     }

     setInterval(tick, 1000);
     ```

190. ### How do you say that props are readonly?

     When you declare a component as a function or a class, it must never modify its own props.

     Let us take a below capital function,

     ```javascript
     function capital(amount, interest) {
       return amount + interest;
     }
     ```

     The above function is called “pure” because it does not attempt to change their inputs, and always return the same result for the same inputs. Hence, React has a single rule saying "All React components must act like pure functions with respect to their props."

191. ### What are the conditions to safely use the index as a key?

     There are three conditions to make sure, it is safe use the index as a key.

     1. The list and items are static– they are not computed and do not change
     2. The items in the list have no ids
     3. The list is never reordered or filtered.

192. ### Should keys be globally unique?

     The keys used within arrays should be unique among their siblings but they don’t need to be globally unique. i.e, You can use the same keys with two different arrays.

     For example, the below `Book` component uses two arrays with different arrays,

     ```javascript
     function Book(props) {
       const index = (
         <ul>
           {props.pages.map((page) => (
             <li key={page.id}>{page.title}</li>
           ))}
         </ul>
       );
       const content = props.pages.map((page) => (
         <div key={page.id}>
           <h3>{page.title}</h3>
           <p>{page.content}</p>
           <p>{page.pageNumber}</p>
         </div>
       ));
       return (
         <div>
           {index}
           <hr />
           {content}
         </div>
       );
     }
     ```

193. ### What is the popular choice for form handling?

     `Formik` is a form library for react which provides solutions such as validation, keeping track of the visited fields, and handling form submission.

     In detail, You can categorize them as follows,

     1. Getting values in and out of form state
     2. Validation and error messages
     3. Handling form submission

     It is used to create a scalable, performant, form helper with a minimal API to solve annoying stuff.

194. ### What are the advantages of formik over redux form library?

     Below are the main reasons to recommend formik over redux form library,

     1. The form state is inherently short-term and local, so tracking it in Redux (or any kind of Flux library) is unnecessary.
     2. Redux-Form calls your entire top-level Redux reducer multiple times ON EVERY SINGLE KEYSTROKE. This way it increases input latency for large apps.
     3. Redux-Form is 22.5 kB minified gzipped whereas Formik is 12.7 kB

195. ### Why are you not required to use inheritance?

     In React, it is recommended to use composition over inheritance to reuse code between components. Both Props and composition give you all the flexibility you need to customize a component’s look and behavior explicitly and safely.
     Whereas, If you want to reuse non-UI functionality between components, it is suggested to extract it into a separate JavaScript module. Later components import it and use that function, object, or class, without extending it.

196. ### Can I use web components in react application?

     Yes, you can use web components in a react application. Even though many developers won't use this combination, it may require especially if you are using third-party UI components that are written using Web Components.

     For example, let us use `Vaadin` date picker web component as below,

     ```javascript
     import "./App.css";
     import "@vaadin/vaadin-date-picker";
     export default function App() {
       return (
         <div className="App">
           <vaadin-date-picker label="When were you born?"></vaadin-date-picker>
         </div>
       );
     }
     ```

197. ### What is dynamic import?

     You can achieve code-splitting in your app using dynamic import.

     Let's take an example of addition,

     1. **Normal Import**

     ```javascript
     import { add } from "./math";
     console.log(add(10, 20));
     ```

     2. **Dynamic Import**

     ```javascript
     import("./math").then((math) => {
       console.log(math.add(10, 20));
     });
     ```

198. ### What are loadable components?

     With the release of React 18, React.lazy and Suspense are now available for server-side rendering. However, prior to React 18, it was recommended to use Loadable Components for code-splitting in a server-side rendered app because React.lazy and Suspense were not available for server-side rendering. Loadable Components lets you render a dynamic import as a regular component. For example, you can use Loadable Components to load the OtherComponent in a separate bundle like this:

     ```javascript
     import loadable from "@loadable/component";

     const OtherComponent = loadable(() => import("./OtherComponent"));

     function MyComponent() {
       return (
         <div>
           <OtherComponent />
         </div>
       );
     }
     ```

     Now OtherComponent will be loaded in a separated bundle
     Loadable Components provides additional benefits beyond just code-splitting, such as automatic code reloading, error handling, and preloading. By using Loadable Components, you can ensure that your application loads quickly and efficiently, providing a better user experience for your users.

199. ### What is suspense component?

     If the module containing the dynamic import is not yet loaded by the time parent component renders, you must show some fallback content while you’re waiting for it to load using a loading indicator. This can be done using **Suspense** component.

     For example, the below code uses suspense component,

     ```javascript
     const OtherComponent = React.lazy(() => import("./OtherComponent"));

     function MyComponent() {
       return (
         <div>
           <Suspense fallback={<div>Loading...</div>}>
             <OtherComponent />
           </Suspense>
         </div>
       );
     }
     ```

     As mentioned in the above code, Suspense is wrapped above the lazy component.

200. ### What is route based code splitting?

     One of the best place to do code splitting is with routes. The entire page is going to re-render at once so users are unlikely to interact with other elements in the page at the same time. Due to this, the user experience won't be disturbed.

     Let us take an example of route based website using libraries like React Router with React.lazy,

     ```javascript
     import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
     import React, { Suspense, lazy } from "react";

     const Home = lazy(() => import("./routes/Home"));
     const About = lazy(() => import("./routes/About"));

     const App = () => (
       <Router>
         <Suspense fallback={<div>Loading...</div>}>
           <Switch>
             <Route exact path="/" component={Home} />
             <Route path="/about" component={About} />
           </Switch>
         </Suspense>
       </Router>
     );
     ```

     In the above code, the code splitting will happen at each route level.

201. ### What is the purpose of default value in context?

     The defaultValue argument is only used when a component does not have a matching Provider above it in the tree. This can be helpful for testing components in isolation without wrapping them.

     Below code snippet provides default theme value as Luna.

     ```javascript
     const MyContext = React.createContext(defaultValue);
     ```

202. ### What is diffing algorithm?

     React needs to use algorithms to find out how to efficiently update the UI to match the most recent tree. The diffing algorithms is generating the minimum number of operations to transform one tree into another. However, the algorithms have a complexity in the order of O(n³) where n is the number of elements in the tree.

     In this case, displaying 1000 elements would require in the order of one billion comparisons. This is far too expensive. Instead, React implements a heuristic O(n) algorithm based on two assumptions:

     1. Two elements of different types will produce different trees.
     2. The developer can hint at which child elements may be stable across different renders with a key prop.

203. ### What are the rules covered by diffing algorithm?

     When diffing two trees, React first compares the two root elements. The behavior is different depending on the types of the root elements. It covers the below rules during reconciliation algorithm,

     1. **Elements Of Different Types:**
        Whenever the root elements have different types, React will tear down the old tree and build the new tree from scratch. For example, elements <a> to <img>, or from <Article> to <Comment> of different types lead a full rebuild.
     2. **DOM Elements Of The Same Type:**
        When comparing two React DOM elements of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes. Lets take an example with same DOM elements except className attribute,

        ```javascript
        <div className="show" title="ReactJS" />

        <div className="hide" title="ReactJS" />
        ```

     3. **Component Elements Of The Same Type:**
        When a component updates, the instance stays the same, so that state is maintained across renders. React updates the props of the underlying component instance to match the new element, and calls componentWillReceiveProps() and componentWillUpdate() on the underlying instance. After that, the render() method is called and the diff algorithm recurses on the previous result and the new result.
     4. **Recursing On Children:**
        when recursing on the children of a DOM node, React just iterates over both lists of children at the same time and generates a mutation whenever there’s a difference. For example, when adding an element at the end of the children, converting between these two trees works well.

        ```javascript
        <ul>
          <li>first</li>
          <li>second</li>
        </ul>

        <ul>
          <li>first</li>
          <li>second</li>
          <li>third</li>
        </ul>

        ```

     5. **Handling keys:**
        React supports a key attribute. When children have keys, React uses the key to match children in the original tree with children in the subsequent tree. For example, adding a key can make the tree conversion efficient,

     ```javascript
     <ul>
       <li key="2015">Duke</li>
       <li key="2016">Villanova</li>
     </ul>

     <ul>
       <li key="2014">Connecticut</li>
       <li key="2015">Duke</li>
       <li key="2016">Villanova</li>
     </ul>
     ```

204. ### When do you need to use refs?

     There are few use cases to go for refs,

     1. Managing focus, text selection, or media playback.
     2. Triggering imperative animations.
     3. Integrating with third-party DOM libraries.

205. ### Must prop be named as render for render props?

     Even though the pattern named render props, you don’t have to use a prop named render to use this pattern. i.e, Any prop that is a function that a component uses to know what to render is technically a “render prop”. Lets take an example with the children prop for render props,

     ```javascript
     <Mouse
       children={(mouse) => (
         <p>
           The mouse position is {mouse.x}, {mouse.y}
         </p>
       )}
     />
     ```

     Actually children prop doesn’t need to be named in the list of “attributes” in JSX element. Instead, you can keep it directly inside element,

     ```javascript
     <Mouse>
       {(mouse) => (
         <p>
           The mouse position is {mouse.x}, {mouse.y}
         </p>
       )}
     </Mouse>
     ```

     While using this above technique(without any name), explicitly state that children should be a function in your propTypes.

     ```javascript
     Mouse.propTypes = {
       children: PropTypes.func.isRequired,
     };
     ```

206. ### What are the problems of using render props with pure components?

     If you create a function inside a render method, it negates the purpose of pure component. Because the shallow prop comparison will always return false for new props, and each render in this case will generate a new value for the render prop. You can solve this issue by defining the render function as instance method.

207. ### What is windowing technique?

     Windowing is a technique that only renders a small subset of your rows at any given time, and can dramatically reduce the time it takes to re-render the components as well as the number of DOM nodes created. If your application renders long lists of data then this technique is recommended. Both react-window and react-virtualized are popular windowing libraries which provides several reusable components for displaying lists, grids, and tabular data.

208. ### How do you print falsy values in JSX?

     The falsy values such as false, null, undefined, and true are valid children but they don't render anything. If you still want to display them then you need to convert it to string. Let's take an example on how to convert to a string,

     ```javascript
     <div>My JavaScript variable is {String(myVariable)}.</div>
     ```

209. ### What is the typical use case of portals?

     React portals are very useful when a parent component has overflow: hidden or has properties that affect the stacking context (e.g. z-index, position, opacity) and you need to visually “break out” of its container.

     For example, dialogs, global message notifications, hovercards, and tooltips.

210. ### How do you set default value for uncontrolled component?

     In React, the value attribute on form elements will override the value in the DOM. With an uncontrolled component, you might want React to specify the initial value, but leave subsequent updates uncontrolled. To handle this case, you can specify a **defaultValue** attribute instead of **value**.

     ```javascript
     render() {
       return (
         <form onSubmit={this.handleSubmit}>
           <label>
             User Name:
             <input
               defaultValue="John"
               type="text"
               ref={this.input} />
           </label>
           <input type="submit" value="Submit" />
         </form>
       );
     }
     ```

     The same applies for `select` and `textArea` inputs. But you need to use **defaultChecked** for `checkbox` and `radio` inputs.

211. ### What is your favorite React stack?

     Even though the tech stack varies from developer to developer, the most popular stack is used in react boilerplate project code. It mainly uses Redux and redux-saga for state management and asynchronous side-effects, react-router for routing purpose, styled-components for styling react components, axios for invoking REST api, and other supported stack such as webpack, reselect, ESNext, Babel.
     You can clone the project https://github.com/react-boilerplate/react-boilerplate and start working on any new react project.

212. ### What is the difference between Real DOM and Virtual DOM?

     Below are the main differences between Real DOM and Virtual DOM,

     | Real DOM                             | Virtual DOM                          |
     | ------------------------------------ | ------------------------------------ |
     | Updates are slow                     | Updates are fast                     |
     | DOM manipulation is very expensive.  | DOM manipulation is very easy        |
     | You can update HTML directly.        | You Can’t directly update HTML       |
     | It causes too much of memory wastage | There is no memory wastage           |
     | Creates a new DOM if element updates | It updates the JSX if element update |

213. ### How to add Bootstrap to a react application?

     Bootstrap can be added to your React app in a three possible ways,

     1. Using the Bootstrap CDN:
        This is the easiest way to add bootstrap. Add both bootstrap CSS and JS resources in a head tag.
     2. Bootstrap as Dependency:
        If you are using a build tool or a module bundler such as Webpack, then this is the preferred option for adding Bootstrap to your React application
        ```javascript
        npm install bootstrap
        ```
     3. React Bootstrap Package:
        In this case, you can add Bootstrap to our React app is by using a package that has rebuilt Bootstrap components to work particularly as React components. Below packages are popular in this category,
        1. react-bootstrap
        2. reactstrap

214. ### Can you list down top websites or applications using react as front end framework?

     Below are the `top 10 websites` using React as their front-end framework,

     1. Facebook
     2. Uber
     3. Instagram
     4. WhatsApp
     5. Khan Academy
     6. Airbnb
     7. Dropbox
     8. Flipboard
     9. Netflix
     10. PayPal

215. ### Is it recommended to use CSS In JS technique in React?

     React does not have any opinion about how styles are defined but if you are a beginner then good starting point is to define your styles in a separate \*.css file as usual and refer to them using className. This functionality is not part of React but came from third-party libraries. But If you want to try a different approach(CSS-In-JS) then styled-components library is a good option.

216. ### Do I need to rewrite all my class components with hooks?

     No. But you can try Hooks in a few components(or new components) without rewriting any existing code. Because there are no plans to remove classes in ReactJS.

217. ### How to fetch data with React Hooks?

     The effect hook called `useEffect` can be used to fetch data from an API and to set the data in the local state of the component with the useState hook’s update function.

     Here is an example of fetching a list of react articles from an API using fetch.

     ```javascript
     import React from "react";

     function App() {
       const [data, setData] = React.useState({ hits: [] });

       React.useEffect(() => {
         fetch("http://hn.algolia.com/api/v1/search?query=react")
           .then((response) => response.json())
           .then((data) => setData(data));
       }, []);

       return (
         <ul>
           {data.hits.map((item) => (
             <li key={item.objectID}>
               <a href={item.url}>{item.title}</a>
             </li>
           ))}
         </ul>
       );
     }

     export default App;
     ```

     A popular way to simplify this is by using the library axios.

     We provided an empty array as second argument to the useEffect hook to avoid activating it on component updates. This way, it only fetches on component mount.

218. ### Is Hooks cover all use cases for classes?

     Hooks doesn't cover all use cases of classes but there is a plan to add them soon. Currently there are no Hook equivalents to the uncommon **getSnapshotBeforeUpdate** and **componentDidCatch** lifecycles yet.

219. ### What is the stable release for hooks support?

     React includes a stable implementation of React Hooks in 16.8 release for below packages

     1. React DOM
     2. React DOM Server
     3. React Test Renderer
     4. React Shallow Renderer

220. ### Why do we use array destructuring (square brackets notation) in `useState`?

     When we declare a state variable with `useState`, it returns a pair — an array with two items. The first item is the current value, and the second is a function that updates the value. Using [0] and [1] to access them is a bit confusing because they have a specific meaning. This is why we use array destructuring instead.

     For example, the array index access would look as follows:

     ```javascript
     var userStateVariable = useState("userProfile"); // Returns an array pair
     var user = userStateVariable[0]; // Access first item
     var setUser = userStateVariable[1]; // Access second item
     ```

     Whereas with array destructuring the variables can be accessed as follows:

     ```javascript
     const [user, setUser] = useState("userProfile");
     ```

221. ### What are the sources used for introducing hooks?

     Hooks got the ideas from several different sources. Below are some of them,

     1. Previous experiments with functional APIs in the react-future repository
     2. Community experiments with render prop APIs such as Reactions Component
     3. State variables and state cells in DisplayScript.
     4. Subscriptions in Rx.
     5. Reducer components in ReasonReact.

222. ### How do you access imperative API of web components?

     Web Components often expose an imperative API to implement its functions. You will need to use a **ref** to interact with the DOM node directly if you want to access imperative API of a web component. But if you are using third-party Web Components, the best solution is to write a React component that behaves as a **wrapper** for your Web Component.

223. ### What is formik?

     Formik is a small react form library that helps you with the three major problems,

     1. Getting values in and out of form state
     2. Validation and error messages
     3. Handling form submission

224. ### What are typical middleware choices for handling asynchronous calls in Redux?

     Some of the popular middleware choices for handling asynchronous calls in Redux eco system are `Redux Thunk, Redux Promise, Redux Saga`.

225. ### Do browsers understand JSX code?

     No, browsers can't understand JSX code. You need a transpiler to convert your JSX to regular Javascript that browsers can understand. The most widely used transpiler right now is Babel.

226. ### Describe about data flow in react?

     React implements one-way reactive data flow using props which reduce boilerplate and is easier to understand than traditional two-way data binding.

227. ### What is MobX?

     MobX is a simple, scalable and battle tested state management solution for applying functional reactive programming (TFRP). For ReactJS application, you need to install below packages,

     ```bash
     npm install mobx --save
     npm install mobx-react --save
     ```

228. ### What are the differences between Redux and MobX?

     Below are the main differences between Redux and MobX,

     | Topic         | Redux                                                         | MobX                                                                   |
     | ------------- | ------------------------------------------------------------- | ---------------------------------------------------------------------- |
     | Definition    | It is a javascript library for managing the application state | It is a library for reactively managing the state of your applications |
     | Programming   | It is mainly written in ES6                                   | It is written in JavaScript(ES5)                                       |
     | Data Store    | There is only one large store exist for data storage          | There is more than one store for storage                               |
     | Usage         | Mainly used for large and complex applications                | Used for simple applications                                           |
     | Performance   | Need to be improved                                           | Provides better performance                                            |
     | How it stores | Uses JS Object to store                                       | Uses observable to store the data                                      |

229. ### Should I learn ES6 before learning ReactJS?

     No, you don’t have to learn es2015/es6 to learn react. But you may find many resources or React ecosystem uses ES6 extensively. Let's see some of the frequently used ES6 features,

     1. **Destructuring:** To get props and use them in a component

        ```javascript
        // in es 5
        var someData = this.props.someData;
        var dispatch = this.props.dispatch;

        // in es6
        const { someData, dispatch } = this.props;
        ```

     2. **Spread operator:** Helps in passing props down into a component

        ```javascript
        // in es 5
        <SomeComponent someData={this.props.someData} dispatch={this.props.dispatch} />

        // in es6
        <SomeComponent {...this.props} />
        ```

     3. **Arrow functions:** Makes compact syntax
        ```javascript
        // es 5
        var users = usersList.map(function (user) {
          return <li>{user.name}</li>;
        });
        // es 6
        const users = usersList.map((user) => <li>{user.name}</li>);
        ```

230. ### What is Concurrent Rendering?

     The Concurrent rendering makes React apps to be more responsive by rendering component trees without blocking the main UI thread. It allows React to interrupt a long-running render to handle a high-priority event. i.e, When you enabled concurrent Mode, React will keep an eye on other tasks that need to be done, and if there's something with a higher priority it will pause what it is currently rendering and let the other task finish first. You can enable this in two ways,

     ```javascript
     // 1. Part of an app by wrapping with ConcurrentMode
     <React.unstable_ConcurrentMode>
       <Something />
     </React.unstable_ConcurrentMode>;

     // 2. Whole app using createRoot
     ReactDOM.unstable_createRoot(domNode).render(<App />);
     ```

231. ### What is the difference between async mode and concurrent mode?

     Both refers the same thing. Previously concurrent Mode being referred to as "Async Mode" by React team. The name has been changed to highlight React’s ability to perform work on different priority levels. So it avoids the confusion from other approaches to Async Rendering.

232. ### Can I use javascript urls in react16.9?

     Yes, you can use javascript: URLs but it will log a warning in the console. Because URLs starting with javascript: are dangerous by including unsanitized output in a tag like `<a href>` and create a security hole.

     ```javascript
     const companyProfile = {
       website: "javascript: alert('Your website is hacked')",
     };
     // It will log a warning
     <a href={companyProfile.website}>More details</a>;
     ```

     Remember that the future versions will throw an error for javascript URLs.

233. ### What is the purpose of eslint plugin for hooks?

     The ESLint plugin enforces rules of Hooks to avoid bugs. It assumes that any function starting with ”use” and a capital letter right after it is a Hook. In particular, the rule enforces that,

     1. Calls to Hooks are either inside a PascalCase function (assumed to be a component) or another useSomething function (assumed to be a custom Hook).
     2. Hooks are called in the same order on every render.

234. ### What is the difference between Imperative and Declarative in React?

     Imagine a simple UI component, such as a "Like" button. When you tap it, it turns blue if it was previously grey, and grey if it was previously blue.

     The imperative way of doing this would be:

     ```javascript
     if (user.likes()) {
       if (hasBlue()) {
         removeBlue();
         addGrey();
       } else {
         removeGrey();
         addBlue();
       }
     }
     ```

     Basically, you have to check what is currently on the screen and handle all the changes necessary to redraw it with the current state, including undoing the changes from the previous state. You can imagine how complex this could be in a real-world scenario.

     In contrast, the declarative approach would be:

     ```javascript
     if (this.state.liked) {
       return <blueLike />;
     } else {
       return <greyLike />;
     }
     ```

     Because the declarative approach separates concerns, this part of it only needs to handle how the UI should look in a specific state, and is therefore much simpler to understand.

235. ### What are the benefits of using TypeScript with ReactJS?

     Below are some of the benefits of using TypeScript with ReactJS,

     1. It is possible to use latest JavaScript features
     2. Use of interfaces for complex type definitions
     3. IDEs such as VS Code was made for TypeScript
     4. Avoid bugs with the ease of readability and Validation

236. ### How do you make sure that user remains authenticated on page refresh while using Context API State Management?

     When a user logs in and reload, to persist the state generally we add the load user action in the useEffect hooks in the main App.js. While using Redux, loadUser action can be easily accessed.

     **App.js**

     ```js
     import { loadUser } from "../actions/auth";
     store.dispatch(loadUser());
     ```

     - But while using **Context API**, to access context in App.js, wrap the AuthState in index.js so that App.js can access the auth context. Now whenever the page reloads, no matter what route you are on, the user will be authenticated as **loadUser** action will be triggered on each re-render.

     **index.js**

     ```js
     import React from "react";
     import ReactDOM from "react-dom";
     import App from "./App";
     import AuthState from "./context/auth/AuthState";

     ReactDOM.render(
       <React.StrictMode>
         <AuthState>
           <App />
         </AuthState>
       </React.StrictMode>,
       document.getElementById("root")
     );
     ```

     **App.js**

     ```js
     const authContext = useContext(AuthContext);

     const { loadUser } = authContext;

     useEffect(() => {
       loadUser();
     }, []);
     ```

     **loadUser**

     ```js
     const loadUser = async () => {
       const token = sessionStorage.getItem("token");

       if (!token) {
         dispatch({
           type: ERROR,
         });
       }
       setAuthToken(token);

       try {
         const res = await axios("/api/auth");

         dispatch({
           type: USER_LOADED,
           payload: res.data.data,
         });
       } catch (err) {
         console.error(err);
       }
     };
     ```

237. ### What are the benefits of new JSX transform?

     There are three major benefits of new JSX transform,

     1. It is possible to use JSX without importing React packages
     2. The compiled output might improve the bundle size in a small amount
     3. The future improvements provides the flexibility to reduce the number of concepts to learn React.

238. ### How is the new JSX transform different from old transform??

     The new JSX transform doesn’t require React to be in scope. i.e, You don't need to import React package for simple scenarios.

     Let's take an example to look at the main differences between the old and the new transform,

     **Old Transform:**

     ```js
     import React from "react";

     function App() {
       return <h1>Good morning!!</h1>;
     }
     ```

     Now JSX transform convert the above code into regular JavaScript as below,

     ```js
     import React from "react";

     function App() {
       return React.createElement("h1", null, "Good morning!!");
     }
     ```

     **New Transform:**

     The new JSX transform doesn't require any React imports

     ```js
     function App() {
       return <h1>Good morning!!</h1>;
     }
     ```

     Under the hood JSX transform compiles to below code

     ```js
     import { jsx as _jsx } from "react/jsx-runtime";

     function App() {
       return _jsx("h1", { children: "Good morning!!" });
     }
     ```

     **Note:** You still need to import React to use Hooks.

239. ### What are React Server components?

     React Server Component is a way to write React component that gets rendered in the server-side with the purpose of improving React app performance. These components allow us to load components from the backend.

     **Note:** React Server Components is still under development and not recommended for production yet.

240. ### What is prop drilling?

     Prop Drilling is the process by which you pass data from one component of the React Component tree to another by going through other components that do not need the data but only help in passing it around.

241. ### What is the difference between useState and useRef hook?

     1. useState causes components to re-render after state updates whereas useRef doesn’t cause a component to re-render when the value or state changes.
        Essentially, useRef is like a “box” that can hold a mutable value in its (.current) property.
     2. useState allows us to update the state inside components. While useRef allows referencing DOM elements.

242. ### What is a wrapper component?

     A wrapper in React is a component that wraps or surrounds another component or group of components. It can be used for a variety of purposes such as adding additional functionality, styling, or layout to the wrapped components.

     For example, consider a simple component that displays a message:

     ```javascript
     const Message = ({ text }) => {
       return <p>{text}</p>;
     };
     ```

     We can create a wrapper component that will add a border to the message component:

     ```javascript
     const MessageWrapper = (props) => {
       return (
         <div style={{ border: "1px solid black" }}>
           <Message {...props} />
         </div>
       );
     };
     ```

     Now we can use the MessageWrapper component instead of the Message component and the message will be displayed with a border:

     ```javascript
     <MessageWrapper text="Hello World" />
     ```

     Wrapper component can also accept its own props and pass them down to the wrapped component, for example, we can create a wrapper component that will add a title to the message component:

     ```javascript
     const MessageWrapperWithTitle = ({ title, ...props }) => {
       return (
         <div>
           <h3>{title}</h3>
           <Message {...props} />
         </div>
       );
     };
     ```

     Now we can use the MessageWrapperWithTitle component and pass title props:

     ```javascript
     <MessageWrapperWithTitle title="My Message" text="Hello World" />
     ```

     This way, the wrapper component can add additional functionality, styling, or layout to the wrapped component while keeping the wrapped component simple and reusable.

243. ### What are the differences between useEffect and useLayoutEffect hooks?

     useEffect and useLayoutEffect are both React hooks that can be used to synchronize a component with an external system, such as a browser API or a third-party library. However, there are some key differences between the two:

     - Timing: useEffect runs after the browser has finished painting, while useLayoutEffect runs synchronously before the browser paints. This means that useLayoutEffect can be used to measure and update layout in a way that feels more synchronous to the user.

     - Browser Paint: useEffect allows browser to paint the changes before running the effect, hence it may cause some visual flicker. useLayoutEffect synchronously runs the effect before browser paints and hence it will avoid visual flicker.

     - Execution Order: The order in which multiple useEffect hooks are executed is determined by React and may not be predictable. However, the order in which multiple useLayoutEffect hooks are executed is determined by the order in which they were called.

     - Error handling: useEffect has a built-in mechanism for handling errors that occur during the execution of the effect, so that it does not crash the entire application. useLayoutEffect does not have this mechanism, and errors that occur during the execution of the effect will crash the entire application.

     In general, it's recommended to use useEffect as much as possible, because it is more performant and less prone to errors. useLayoutEffect should only be used when you need to measure or update layout, and you can't achieve the same result using useEffect.

244. ### What are the differences between Functional and Class Components?

     There are two different ways to create components in ReactJS. The main differences are listed down as below,

     ## 1. Syntax:

     The class components uses ES6 classes to create the components. It uses `render` function to display the HTML content in the webpage.

     The syntax for class component looks like as below.

     ```js
     class App extends React.Component {
       render() {
         return <h1>This is a class component</h1>;
       }
     }
     ```

     **Note:** The **Pascal Case** is the recommended approach to provide naming to a component.

     Functional component has been improved over the years with some added features like Hooks. Here is a syntax for functional component.

     ```js
     function App() {
       return (
         <div className="App">
           <h1>Hello, I'm a function component</h1>
         </div>
       );
     }
     ```

     ## 2. State:

     State contains information or data about a component which may change over time.

     In class component, you can update the state when a user interacts with it or server updates the data using the `setState()` method. The initial state is going to be assigned in the `Constructor()` method using the `this.state` object and it is possible to assign different data types such as string, boolean, numbers, etc.

     **A simple example showing how we use the setState() and constructor():**

     ```js
     class App extends Component {
       constructor() {
         super();
         this.state = {
           message: "This is a class component",
         };
       }
       updateMessage() {
         this.setState({
           message: "Updating the class component",
         });
       }
       render() {
         return (
           <>
             <h1>{this.state.message}</h1>
             <button
               onClick={() => {
                 this.updateMessage();
               }}
             >
               Click!!
             </button>
           </>
         );
       }
     }
     ```

     You didn't use state in functional components because it was only supported in class components. But over the years hooks have been implemented in functional components which enables to use state too.

     The `useState()` hook can used to implement state in functional components. It returns an array with two items: the first item is current state and the next one is a function (setState) that updates the value of the current state.

     Let's see an example to demonstrate the state in functional components,

     ```js
     function App() {
       const [message, setMessage] = useState("This is a functional component");
       const updateMessage = () => {
         setMessage("Updating the functional component");
       };
       return (
         <div className="App">
           <h1>{message} </h1>
           <button onClick={updateMessage}>Click me!!</button>
         </div>
       );
     }
     ```

     ## 3. Props:

     Props are referred to as "properties". The props are passed into React component just like arguments passed to a function. In other words, they are similar to HTML attributes.

     The props are accessible in child class component using `this.props` as shown in below example,

     ```js
     class Child extends React.Component {
       render() {
         return (
           <h1>
             {" "}
             This is a functional component and component name is {
               this.props.name
             }{" "}
           </h1>
         );
       }
     }

     class Parent extends React.Component {
       render() {
         return (
           <div className="Parent">
             <Child name="First child component" />
             <Child name="Second child component" />
           </div>
         );
       }
     }
     ```

     Props in functional components are similar to that of the class components but the difference is the absence of 'this' keyword.

     ```js
     function Child(props) {
       return (
         <h1>
           This is a child component and the component name is{props.name}
         </h1>
       );
     }

     function Parent() {
       return (
         <div className="Parent">
           <Child name="First child component" />
           <Child name="Second child component" />
         </div>
       );
     }
     ```

245. ### What is strict mode in React?

     `React.StrictMode` is a useful component for highlighting potential problems in an application. Just like `<Fragment>`, `<StrictMode>` does not render any extra DOM elements. It activates additional checks and warnings for its descendants. These checks apply for _development mode_ only.

     ```jsx harmony
     import { StrictMode } from "react";

     function App() {
       return (
         <div>
           <Header />
           <StrictMode>
             <div>
               <ComponentOne />
               <ComponentTwo />
             </div>
           </StrictMode>
           <Header />
         </div>
       );
     }
     ```

     In the example above, the _strict mode_ checks apply to `<ComponentOne>` and `<ComponentTwo>` components only. i.e., Part of the application only.

     **Note:** Frameworks such as NextJS has this flag enabled by default.

246. ### What is the benefit of strict mode?

     The <StrictMode> will be helpful in the below cases,

     1. To find the bugs caused by impure rendering where the components will re-render twice.
     2. To find the bugs caused by missing cleanup of effects where the components will re-run effects one more extra time.
     3. Identifying components with **unsafe lifecycle methods**.
     4. Warning about **legacy string ref** API usage.
     5. Detecting unexpected **side effects**.
     6. Detecting **legacy context** API.
     7. Warning about deprecated **findDOMNode** usage

247. ### Why does strict mode render twice in React?

     StrictMode renders components twice in development mode(not production) in order to detect any problems with your code and warn you about those problems. This is used to detect accidental side effects in the render phase. If you used `create-react-app` development tool then it automatically enables StrictMode by default.

     ```js
     const root = createRoot(document.getElementById("root"));
     root.render(
       <StrictMode>
         <App />
       </StrictMode>
     );
     ```

     If you want to disable this behavior then you can simply remove `strict` mode.

     ```js
     const root = createRoot(document.getElementById("root"));
     root.render(<App />);
     ```

     To detect side effects the following functions are invoked twice:

     1. Function component bodies, excluding the code inside event handlers.
     2. Functions passed to `useState`, `useMemo`, or `useReducer` (any other Hook)
     3. Class component's `constructor`, `render`, and `shouldComponentUpdate` methods
     4. Class component static `getDerivedStateFromProps` method
     5. State updater functions

248. ### What are the rules of JSX?

     The below 3 rules needs to be followed while using JSX in a react application.

     1. **Return a single root element**:
        If you are returning multiple elements from a component, wrap them in a single parent element. Otherwise you will receive the below error in your browser console.

        `html Adjacent JSX elements must be wrapped in an enclosing tag.`

     2. **All the tags needs to be closed:**
        Unlike HTML, all tags needs to closed explicitly with in JSX. This rule applies for self-closing tags(like hr, br and img tags) as well.
     3. **Use camelCase naming:**
        It is suggested to use camelCase naming for attributes in JSX. For example, the common attributes of HTML elements such as `class`, `tabindex` will be used as `className` and `tabIndex`.  
        **Note:** There is an exception for `aria-*` and `data-*` attributes which should be lower cased all the time.

249. ### What is the reason behind multiple JSX tags to be wrapped?

     Behind the scenes, JSX is transformed into plain javascript objects. It is not possible to return two or more objects from a function without wrapping into an array. This is the reason you can't simply return two or more JSX tags from a function without
     wrapping them into a single parent tag or a Fragment.

250. ### How do you prevent mutating array variables?

     The preexisting variables outside of the function scope including state, props and context leads to a mutation and they result in unpredictable bugs during the rendering stage. The below points should be taken care while working with arrays variables.

     1. You need to take copy of the original array and perform array operations on it for the rendering purpose. This is called local mutation.
     2. Avoid triggering mutation methods such as push, pop, sort and reverse methods on original array. It is safe to use filter, map and slice method because they create a new array.

251. ### What are capture phase events?

     The `onClickCapture` React event is helpful to catch all the events of child elements irrespective of event propagation logic or even if the events propagation stopped. This is useful if you need to log every click events for analytics purpose.

     For example, the below code triggers the click event of parent first followed by second level child eventhough leaf child button elements stops the propagation.

     ```jsx
     <div onClickCapture={() => alert("parent")}>
       <div onClickCapture={() => alert("child")}>
         <button onClick={(e) => e.stopPropagation()} />
         <button onClick={(e) => e.stopPropagation()} />
       </div>
     </div>
     ```

     The event propagation for the above code snippet happens in the following order:

     1. It travels downwards in the DOM tree by calling all `onClickCapture` event handlers.
     2. It executes `onClick` event handler on the target element.
     3. It travels upwards in the DOM tree by call all `onClick` event handlers above to it.

252. ### How does React updates screen in an application?

     React updates UI in three steps,

     1. **Triggering or initiating a render:** The component is going to triggered for render in two ways.

        1. **Initial render:** When the app starts, you can trigger the initial render by calling `creatRoot` with the target DOM node followed by invoking component's `render` method. For example, the following code snippet renders `App` component on root DOM node.

        ```jsx
        import { createRoot } from "react-dom/client";

        const root = createRoot(document.getElementById("root"));
        root.render(<App />);
        ```

        2. **Re-render when the state updated:** When you update the component state using the state setter function, the componen't state automatically queues for a render.

     2. **Rendering components:** After triggering a render, React will call your components to display them on the screen. React will call the root component for initial render and call the function component whose state update triggered the render. This is a recursive process for all nested components of the target component.

     3. **Commit changes to DOM:** After calling components, React will modify the DOM for initial render using `appendChild()` DOM API and apply minimal necessary DOM updates for re-renders based on differences between rerenders.

253. ### How does React batch multiple state updates?

     React prevents component from re-rendering for each and every state update by grouping multiple state updates within an event handler. This strategy improves the application performance and this process known as **batching**. The older version of React only supported batching for browser events whereas React18 supported for asynchronous actions, timeouts and intervals along with native events. This improved version of batching is called **automatic batching**.

     Let's demonstrate this automatic batching feature with a below example.

     ```jsx
     import { useState } from "react";

     export default function BatchingState() {
       const [count, setCount] = useState(0);
       const [message, setMessage] = useState("batching");

       console.log("Application Rendered");

       const handleUsers = () => {
         fetch("https://jsonplaceholder.typicode.com/users/1").then(() => {
           // Automatic Batching re-render only once
           setCount(count + 1);
           setMessage("users fetched");
         });
       };

       return (
         <>
           <h1>{count}</h1>
           <button onClick={handleAsyncFetch}>Click Me!</button>
         </>
       );
     }
     ```

     The preceding code updated two state variables with in an event handler. However, React will perform automatic batching feature and the component will be re-rendered only once for better performance.

254. ### Is it possible to prevent automatic batching?

     Yes, it is possible to prevent automatic batching default behavior. There might be cases where you need to re-render your component after each state update or updating one state depends on another state variable. Considering this situation, React introduced `flushSync` method from `react-dom` API for the usecases where you need to flush state updates to DOM immediately.

     The usage of `flushSync` method within an `onClick` event handler will be looking like as below,

     ```jsx
     import { flushSync } from "react-dom";

     const handleClick = () => {
       flushSync(() => {
         setClicked(!clicked); //Component will create a re-render here
       });

       setCount(count + 1); // Component will create a re-render again here
     };
     ```

     In the above click handler, React will update DOM at first using flushSync and second time updates DOM because of the counter setter function by avoiding automatic batching.

255. ### What is React hydration?

     React hydration is used to add client-side JavaScript interactivity to pre-rendered static HTML generated by the server. It is used only for server-side rendering(SSR) to enhance the initial rendering time and make it SEO friendly application. This hydration acts as a bridge to reduce the gap between server side and client-side rendering.

     After the page loaded with generated static HTML, React will add application state and interactivity by attaching all event handlers for the respective elements. Let's demonstrate this with an example.

     Consider that React DOM API(using `renderToString`) generated HTML for `<App>` component which contains `<button>` element to increment the counter.

     ```jsx
     import {useState} from 'react';
     import { renderToString } from 'react-dom/server';

     export default function App() {
       const [count, setCount] = React.useState(0);

       return (
         <h1>Counter</h1>
         <button onClick={() => setCount(prevCount => prevCount + 1)}>
           {count} times
         </button>
         );
     }

     const html = renderToString(<App />);
     ```

     The above code generates the below HTML with a header text and button component without any interactivity.

     ```html
     <h1>Counter</h1>
     <button>
       <!-- -->0<!-- -->
       times
     </button>
     ```

     At this stage `hydrateRoot` API can be used to perform hydration by attaching `onClick` event handler.

     ```jsx
     import { hydrateRoot } from "react-dom/client";
     import App from "./App.js";

     hydrateRoot(document.getElementById("root"), <App />);
     ```

     After this step, you are able to run React application on server-side and hydrating the javascript bundle on client-side for smooth user experience and SEO purposes.

256. ### How do you update objects inside state?

     You cannot update the objects which exists in the state directly. Instead, you should create a fresh new object (or copy from the existing object) and update the latest state using the newly created object. Eventhough JavaScript objects are mutable, you need to treat objects inside state as read-only while updating the state.

     Let's see this comparison with an example. The issue with regular object mutation approach can be described by updating the user details fields of `Profile` component. The properties of `Profile` component such as firstName, lastName and age details mutated in an event handler as shown below.

     ```jsx
     import { useState } from "react";

     export default function Profile() {
       const [user, setUser] = useState({
         firstName: "John",
         lastName: "Abraham",
         age: 30,
       });

       function handleFirstNameChange(e) {
         user.firstName = e.target.value;
       }

       function handleLastNameChange(e) {
         user.lastName = e.target.value;
       }

       function handleAgeChange(e) {
         user.age = e.target.value;
       }

       return (
         <>
           <label>
             First name:
             <input value={user.firstName} onChange={handleFirstNameChange} />
           </label>
           <label>
             Last name:
             <input value={user.lastName} onChange={handleLastNameChange} />
           </label>
           <label>
             Age:
             <input value={user.age} onChange={handleAgeChange} />
           </label>
           <p>
             Profile:
             {person.firstName} {person.lastName} ({person.age})
           </p>
         </>
       );
     }
     ```

     Once you run the application with above user profile component, you can observe that user profile details won't be update upon entering the input fields.
     This issue can be fixed by creating a new copy of object which includes existing properties through spread syntax(...obj) and add changed values in a single event handler itself as shown below.

     ```jsx
     handleProfileChange(e) {
       setUser({
       ...user,
         [e.target.name]: e.target.value
       });
     }
     ```

     The above event handler is concise instead of maintaining separate event handler for each field. Now, UI displays the updated field values as expected without an issue.

257. ### How do you update nested objects inside state?

     You cannot simply use spread syntax for all kinds of objects inside state. Because spread syntax is shallow and it copies properties for one level deep only. If the object has nested object structure, UI doesn't work as expected with regular JavaScript nested property mutation. Let's demonstrate this behavior with an example of User object which has address nested object inside of it.

     ```jsx
     const user = {
       name: "John",
       age: 32,
       address: {
         country: "Singapore",
         postalCode: 440004,
       },
     };
     ```

     If you try to update the country nested field in a regular javascript fashion(as shown below) then user profile screen won't be updated with latest value.

     ```js
     user.address.country = "Germany";
     ```

     This issue can be fixed by flattening all the fields into a top-level object or create a new object for each nested object and point it to it's parent object. In this example, first you need to create copy of address object and update it with the latest value. Later, the address object should be linked to parent user object something like below.

     ```js
     setUser({
       ...user,
       address: {
         ...user.address,
         country: "Germany",
       },
     });
     ```

     This approach is bit verbose and not easy for deep hierarchical state updates. But this workaround can be used for few levels of nested objects without much hassle.

258. ### How do you update arrays inside state?

     Eventhough arrays in JavaScript are mutable in nature, you need to treat them as immutable while storing them in a state. That means, similar to objects, the arrays cannot be updated directly inside state. Instead, you need to create a copy of the existing array and then set the state to use newly copied array.

     To ensure that arrays are not mutated, the mutation operations like direct direct assignment(arr[1]='one'), push, pop, shift, unshift, splice etc methods should be avoided on original array. Instead, you can create a copy of existing array with help of array operations such as filter, map, slice, spread syntax etc.

     For example, the below push operation doesn't add the new todo to the total todo's list in an event handler.

     ```jsx
     onClick = {
       todos.push({
         id: id+1,
         name: name
       })
     }
     ```

     This issue is fixed by replacing push operation with spread syntax where it will create a new array and the UI updated with new todo.

     ```jsx
     onClick = {
       [
         ...todos,
         { id: id+1, name: name }
       ]
     }
     ```

259. ### How do you use immer library for state updates?

     Immer library enforces the immutability of state based on **copy-on-write** mechanism. It uses JavaScript proxy to keep track of updates to immutable states. Immer has 3 main states as below,

     1. **Current state:** It refers to actual state
     2. **Draft state:** All new changes will be applied to this state. In this state, draft is just a proxy of the current state.
     3. **Next state:** It is formed after all mutations applied to the draft state

     Immer can be used by following below instructions,

     1. Install the dependency using `npm install use-immer` command
     2. Replace `useState` hook with `useImmer` hook by importing at the top
     3. The setter function of `useImmer` hook can be used to update the state.

     For example, the mutation syntax of immer library simplifies the nested address object of user state as follows,

     ```jsx
     import { useImmer } from "use-immer";
     const [user, setUser] = useImmer({
       name: "John",
       age: 32,
       address: {
         country: "Singapore",
         postalCode: 440004,
       },
     });

     //Update user details upon any event
     setUser((draft) => {
       draft.address.country = "Germany";
     });
     ```

     The preceding code enables you to update nested objects with a conceise mutation syntax.

260. ### What are the benefits of preventing the direct state mutations?

261. ### What are the preferred and non-preferred array operations for updating the state?

     The below table represent preferred and non-preferred array operations for updating the component state.

     | Action    | Preferred            | Non-preferred              |
     | --------- | -------------------- | -------------------------- |
     | Adding    | concat, [...arr]     | push, unshift              |
     | Removing  | filter, slice        | pop, shift, splice         |
     | Replacing | map                  | splice, arr[i] = someValue |
     | sorting   | copying to new array | reverse, sort              |

     If you use Immer library then you can able to use all array methods without any problem.

262. ### What will happen by defining nested function components?

Technically it is possible to write nested function components but it is not suggested to write nested function definitions. Because it leads to unexpected bugs and performance issues.

263.  ### Can I use keys for non-list items?

      Keys are primarily used for rendering list items but they are not just for list items. You can also use them React to distinguish components. By default, React uses order of the components in

264.  ### What are the guidelines to be followed for writing reducers?

      There are two guidelines to be taken care while writing reducers in your code.

      1. Reducers must be pure without mutating the state. That means, same input always returns the same output. These reducers run during rendering time similar to state updater functions. So these functions should not send any requests, schedule time outs and any other side effects.

      2. Each action should describe a single user interaction eventhough there are multiple changes applied to data. For example, if you "reset" registration form which has many user input fields managed by a reducer, it is suggested to send one "reset" action instead of creating separate action for each fields. The proper ordering of actions should reflect the user interactions in the browser and it helps a lot for debugging purpose.

265.  ### What is useReducer hook? Can you describe its usage?

266.  ### How do you compare useState and useReducer?

267.  ### How does context work using the useContext hook?

      The `useContext` hook in React is a way to access the context values directly in functional components without needing to wrap them in a consumer component. It simplifies the process of subscribing to context changes.

      To use `useContext`, you first need to create a context using `React.createContext()`. This context object will hold the default value and be used to provide and consume the context values.

      Example usage:

      ```jsx
      import React, { useContext } from "react";

      const MyContext = React.createContext();

      const MyComponent = () => {
        const contextValue = useContext(MyContext);
        return <div>{contextValue}</div>;
      };

      const App = () => (
        <MyContext.Provider value="Hello, World!">
          <MyComponent />
        </MyContext.Provider>
      );
      ```

      In this example, `MyComponent` uses the `useContext` hook to access the value provided by `MyContext.Provider`. When `App` renders, `MyComponent` will display "Hello, World!".

268.  ### What are the use cases of useContext hook?

      Some of the common use cases of useContext are listed below,

      1. **Theme customizations:** The useContext hook can be used to manage and apply custom themes for an application. That means it allows users to personalize the appearance of the application.
      2. **Support localization:** The context hook is helpful to implement localization by providing translated strings to components based on the user's language/locale preference.
      3. **User authentication:** It can be used to manage user authentication or session status and display user specific information with in components.

269.  ### When to use client and server components?

      You can efficiently build nextjs application if you are aware about which part of the application needs to use client components and which other parts needs to use server components. The common cases of both client and server components are listed below:

      **Client components:**

      1. Whenever your need to add interactivity and event listeners such as onClick(), onChange(), etc to the pages
      2. If you need to use State and Lifecycle Effects like useState(), useReducer(), useEffect() etc.
      3. If there is a requirement to use browser-only APIs.
      4. If you need to implement custom hooks that depend on state, effects, or browser-only APIs.
      5. There are React Class components in the pages.

      **Server components:**

      1. If the component logic is about data fetching.
      2. If you need to access backend resources directly.
      3. When you need to keep sensitive information((access tokens, API keys, etc) ) on the server.
      4. If you want reduce client-side JavaScript and placing large dependencies on the server.

270.  ### What are the differences between page router and app router in nextjs?
      /**\*\***\***\*\*** ✨ Codeium Command ⭐ **\*\***\***\*\***/
271.  ### What are the differences between page router and app router in nextjs?

           Next.js provides two types of routers: page router and app router. Page router is used to navigate between pages in the application, while app router is used to navigate between different routes in the application.

      /**\*\*** ceca896d-12db-4eda-85b2-81bf5a6c9ada **\*\*\***/

/**\*\***\***\*\*** ✨ Codeium Command ⭐ **\*\***\***\*\***/
</br>
/**\*\*** 9aa7abb0-ee6a-40ae-9cad-a6bcb4c7ffc6 **\*\*\***/

### Javascript

- https://jsonplaceholder.typicode.com/todos => For dummy data for get request
- https://dummyjson.com/docs/products => For dummy data for other CURD request

- document.write() --> don't use it after the document is loaded
- window.print() --> To print the page
- You can also declare multiple variables in single line:
- - let person = "John Doe", carName = "Volvo", price = 200;
- A variable declared without a value will have the value undefined. - let carName;
- let: have Block Scope, must be Declared before use, cannot be Redeclared in the same scope

- Always use const for new Array, Object, Function, RegEx

- String compares alphabetically:

```bash

- let x = "5" + 2 + 3; # 523
- let x = 2 + 3 + "5"; # 55

console.log("2", 2)
console.log("2"+ 2)

let text1 = "A";
let text2 = "B";
let result = text1 < text2; # returns true

let text1 = "20";
let text2 = "5";
let result = text1 < text2; # returns true
```

- typeof vs instanceOf =>

```bash
# Use instanceof for custom types:
var ClassFirst = function () {};
var instance = new ClassFirst();
instance instanceof ClassFirst; // true
# Use instanceof for complex built in types:
/regularexpression/ instanceof RegExp; // true

# Use typeof for simple built in types:
typeof true == 'boolean'; // true
typeof 99.99 == 'number'; // true
typeof "John";            // Returns "string"
typeof 3.14;              // Returns "number"
typeof (3);               // Returns "number"
typeof (3 + 4);           // Returns "number"
```

- Logical AND operator, Logical OR operator, Nullish coalescing operator

  - && => If the first value is true, the second value is assigned.
  - || => If the first value is false, the second value is assigned.
  - ?? => If the first value is undefined or null, the second value is assigned.

- 8 Datatypes: String,Number, Bigint, Boolean, Undefined, Null, Symbol, Object

  - The object data type can contain both built-in objects, and user defined objects:
  - objects, arrays, dates, maps, sets, intarrays, floatarrays, promises, maths, functions,.. are build-in objects (All JavaScript values, except primitives, are objects.)

```bash
# exponential notation
let y = 123e5;    // 12300000
let z = 123e-5;   // 0.00123
```

- Objects: https://www.w3schools.com/jsref/jsref_obj_object.asp (for more info/methods)

```bash
# Create an empty Objects
const person = {}; # 1st way
const person = new Object(); # 2nd way

# fullName is a method (same as function)
const person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  # // this refers to person object (if properties of person changes then the value of this also changes)
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
  myCars: {
    car1:"Ford",
    car2:"BMW",
    car3:"Fiat"
  }
};

# accessing the objects
person.lastName;
person["lastName"];
let x = "lastName";
person[x];

# updating the objects
person.lastname = "Meo";

# Add new properties
person.nationality = "English";

# deleting a properties
delete person.lastname; // (or) delete person["age"];

# accessing nested objects
myObj.myCars.car2;
myObj.myCars["car2"];
myObj["myCars"]["car2"];
myObj["myCars"].car2;

# accessing object method
name = person.fullName();
```

- Objects are mutable: They are addressed by reference, not by value.

```bash
// Create an Object
const person = {
  firstName:"John",
  lastName:"Doe",
  age:50,
}

// Create a copy
const x = person;

// Change Age in both
x.age = 10; # This will change the value in both the person and x.
```

- How to Display JavaScript Objects?

  1. Displaying the Object Properties by name
  2. Displaying the Object Properties in a Loop
  3. Displaying the Object using Object.values()
  4. Displaying the Object using JSON.stringify()

```bash
# 1
person.name

# 2
let text = "";
for (let x in person) {
    text += person[x] + " ";
}

# 3
const myArray = Object.values(person); // ['John', 'Deo', 50]
const myArray = Object.keys(person); // ['firstName', 'lastName', age]
const myArray = Object.entries(person); // [ [ 'firstName', 'John' ], [ 'lastName', 'Deo' ], [ 'age', 50 ] ]

# 4
JSON.stringify(person)

# Find a length of object
const size = Object.keys(person).length;
```

- Object Constructor:

```bash

# Create a Object Type Person (Constructor) -> USING FUNCTION
function Person(first, last, age) {
  this.firstName = first; // this value will be created by new person objects
  this.lastName = last;
  this.age = age;
  this.eyeColor = Blue; // This value is default (ie. available to everyone)
  this.fullName = function() {
    return this.firstName + " " + this.lastName;
  };
}

# create new Person objects
const myFather = new Person("John", "Doe", 50);
const myMother = new Person("Sally", "Rally", 48);

# Adding a Property to an Object
myFather.nationality = "English";

# Adding a Property to a Constructor
Person.prototype.state = "Goa"; # cannot write Person.nationality = "English";
  # - IT CAN'T BE VISIBLE IN LOG BUT CAN BE ACCESS BY .(DOT)
  console.log(myFather); # This won't include state BUT
  console.log(myFather.state); # This will give Goa

# Adding a Method to an Object
myMother.changeName = function (name) {
  this.lastName = name;
}
# Adding a Method to an Constructor
Person.prototype.changeName = function (name) {
  this.lastName = name;
}
myMother.changeName("Doe"); // Then simply type this to call a method

# Built-in JavaScript Constructors
new Object();   // A new Object object =or=> {}
new Array();    // A new Array object =or=> []
new Map();      // A new Map object
new Set();      // A new Set object
new Date();     // A new Date object
new RegExp();   // A new RegExp object =or=> /()/
new Function(); // A new Function object =or=> () {}

#NOTE:: The Math() object is not in the list. Math is a global object. The new keyword cannot be used on Math.
```

- JavaScript Strings as Objects: (Avoid this -> new String())

```bash
# String objects can produce unexpected results and slows down execution speed.
let x = "John";
let y = new String("John");
x === y; // false

let z = new String("John");
x == z; x === z; // Both will return false

#NOTE:: Comparing two JavaScript objects always returns false.
```

- Javascript strings are primitive and immutable: All string methods produces a new string without altering the original string.

- STRING METHODS

```bash
let text = "HELLO WORLD";
let length = text.length; # returns length
let char = text.charAt(0); # returns charcter at 0 =>>
let char = text.charCodeAt(0); # returns ASIIC Codde at 0
let letter = name.at(2); # returns charcter at 2 ==>> ALLOW -VE INDEXING
let letter = name[2]; # returns charcter at 2 [AVOID THIS] --USE CHARAT OR AT()
# REVISE
# slice(start, end)
# substring(start, end) # SAME as slice but values less than 0 are treated as 0 in substring().
let part = text.slice(7);
let part = text.slice(7, 8); # only one number selected
let part = text.slice(-2); # only last two
# substr(start, length)

let text2 = text1.toUpperCase();
let text2 = text1.toLowerCase();.

let text3 = text1.concat(" ", text2);
let text3 = "Hello" + " " + "World!"; # same as above
console.log([1, 2] + [3, 4]); # 1,23,4
# The + operator is not meant or defined for arrays. So it converts arrays into strings and concatenates them.

let text2 = text1.trim(); # remove spaces from both side
let text2 = text1.trimStart();
let text2 = text1.trimEnd();

let text = "5";
let padded = text.padStart(4,"0"); # 0005 # it will add 0 untill it find 4th position
let padded = text.padStart(4,"x"); # xxx5
let padded = text.padEnd(4,"x"); # 5xxx
let padded = text.padEnd(4,"abcdefg"); # 5abc

let text = "Hello world!";
let result = text.repeat(4); # Hello world!Hello world!Hello world!Hello world!

let text = "Please visit Microsoft and Microsoft!";
let newText = text.replace("Microsoft", "W3Schools"); # only 1st Microsoft is replaced
let newText = text.replace(/Microsoft/g, "W3Schools"); # TO REPLACE ALL (regex is used)
let newText = text.replaceAll(Microsoft, "W3Schools"); # REPLACE ALL
let newText = text.replace("MICROSOFT", "W3Schools"); # WON'T REPLACE AS CASE SENSITIVE
let newText = text.replace(/MICROSOFT/i, "W3Schools"); # USE REGEX FOR CASE INSENSITIVE

let newText = text.split(" ") #["Hello", "world!"] create arr # can do with "o" or ""

let text = "Please locate where 'locate' occurs!";
let index = text.indexOf("locate"); # 7 # will return 1st occurance or -1
let index = text.indexOf("locate", 15); # 21 AS IT WILL START COUNTING FROM 15
let index = text.lastIndexOf("locate"); # 21 # will return last occurance or -1
let index = text.search("locate"); # same as indexOf
let index = text.search(/Locate/i);
# The search() method cannot take a second start position argument.
# The indexOf() method cannot take powerful search values (regular expressions).
# BOTH SEARCH() AND INDEXOF() WILL RETURN -1 IF NO VALUE IS FOUND
let numbers = [1, 2, 3, 4, NaN];
console.log(numbers.indexOf(NaN));                                                # -1
# The indexOf uses strict equality operator(===) internally and NaN === NaN evaluates to false. Since indexOf won't be able to find NaN inside an array, it returns -1 always.

let text = "The rain in SPAIN stays mainly in the plain";
let newText = text.match("ain"); # ["ain", index:5,input:"the...plain",group:]
let newText = text.match(/ain/gi); # [ 'ain', 'AIN', 'ain', 'ain' ]
let newText = text.matchAll('ain'); # provide all array of same match
# this will give array of array[["ain", index:5,input:"the...plain",group:]..[]]
  for (let x of newText) {
    console.log(x);
  }
# REVISE
# includes, startWith, and endsWith are case sensitive
let text = "Hello world, welcome to the universe.";
let newText = text.includes("world"); # true # will return true if text exists
let newText = text.includes("world", 12); # false # starts from 12 index

let newText = text.startsWith("Hello"); # true # as it start with Hello
let newText = text.startsWith("world", 6) # true # as at 6th index it start with world
let newText = text.endsWith("universe"); # true # as it ends with universe
let newText = text.endsWith("world", 11); # true # as at 11th index it ends with world

```

- Numeric Strings

```bash
# Only + will convert number to string
let x = 10;
let y = 20;
let z = "The result is: " + x + y; # not 30 but 1020

let x = "100"; # IT WILL WORK AS NUMBER IF NOT ADDED (ELSE IF 100E THEN NaN)
let y = "10";
let z = x / y; # return 10 (work as number)
let z = x * y; # return 1000 (work as number)
let z = x - y; # return 90 (work as number)
let z = x + y; # return 10010 (work as string)
```

- NaN - Not a Number && Infinity

```bash
let x = 100 / "Apple"; # NaN
isNaN(x); # true
typeof NaN; # number # NaN is a number
let x =  2 / 0; # Infinity # Infinity is a number

let x = 0xFF; # x = 255 # write 0x to before to write hexadecimal number

let myNumber = 255;
myNumber.toString(32); # 7v
myNumber.toString(16); # ff # converted to hexadecimal
myNumber.toString(12); # 193
myNumber.toString(10); # 255 # By default, JS displays numbers as base 10 decimals
myNumber.toString(8); # 377
myNumber.toString(2); # 11111111 # converted to binary

let x = 500;
let y = new Number(500);
x == y; # true
x === y; # false

let z = new Number(500);
x == y; x === y; # both are false as Comparing two JS objects always returns false.

let x = 1234567890123456789012345n; # write n at end to create BigInt
let y = BigInt(1234567890123456789012345) # write this to create BigInt
let hex = 0x20000000000003n; # BigInt in hexadecimal

let x = 5n; # BigInt
let y = x / 2; #==> Error: Cannot mix BigInt and other types, use explicit conversion.
let y = Number(x) / 2; # Convert to number
console.log(y);

let x = Number.MAX_SAFE_INTEGER; # (9007199254740991) gives max integer that is safe to work with
let x = Number.MIN_SAFE_INTEGER; # (-9007199254740991) gives min integer that is safe to work with
Number.isInteger(10); # returns true -> IT CHECKS ONLY WHOLE NUMBER
Number.isInteger(10.5); # returns false (as not integer but float or decimal)
Number.isInteger(12345678901234567890); # returns true
Number.isSafeInteger(12345678901234567890); # returns false

# REVISE
const x = 223.24;
Number.isFinite(x); #(true) Checks whether a value is a finite number
Number.isInteger(x); #(false) Checks whether a value is an integer
Number.isNaN(x); #(false) Checks whether a value is Number.NaN
Number.parseFloat(x); #(223.24) Parses a string an returns a number
Number.parseInt(x); #(223) 	Parses a string an returns a whole number
x.toFixed(4); #(223.2400) [ONLY NUMBERS][ROUND-VALUE] 4 numbers of digits after decimal point
x.toPrecision(4); #(223.2) [ONLY NUMBERS][ROUND-VALUE] Total 4 numbers with or without decimal
x.toString(10); #(223.24) Converts a number to a string -OPTINAL (BASE CONVERSION (2 to 32))- radix
```

- String Methods

```bash

toString(), toExponential(), toFixed(), toPrecision() --> all returns string

let x = 123;
x.toString(); # Converts a number to a string

let x = 912342134.656;
x.toExponential(); # 9.12342134656e+8
x.toExponential(2); # 9.12e+8
x.toExponential(4); # 9.1234e+8
x.toExponential(6); # 9.123421e+8

let x = 921.656;
x.toFixed(0); # 922
x.toFixed(2); # 921.66
x.toFixed(4); # 921.6560
x.toFixed(6); # 921.656000

let x = 92.656;
x.toPrecision(); # 92.656
x.toPrecision(2); # 93
x.toPrecision(4); # 92.66
x.toPrecision(6); # 92.6560

# REVISE
Number(true);                                                               # 1
Number(false);                                                              # 0
Number("-10");                                                              # -10
Number("  10");                                                             # 10
Number("10  ");                                                             # 10
Number("10  10");                                                           # NaN
Number(" 10  ");                                                            # 10
Number("10.33");                                                            # 10.33
Number("10,33");                                                            # NaN
Number("10 33");                                                            # NaN
Number("John");                                                             # NaN

# parses string to whole number. Spaces are allowed. Only the first number is returned:
parseInt("-10");                    # -10
parseInt("-10.33");                 # -10
parseInt("10");                     # 10
parseInt("10.33");                  # 10
parseInt("10 20 30");               # 10
parseInt("10 years");               # 10
parseFloat("10,10 years");          # 10
parseInt("years 10");               # NaN

Number("10  10");                                                           # NaN
parseInt("10  10");                                                         # 10

# parseInt(string, radix) # radix is number from 2 to 32 for base number system
parseInt("0xF", 16);                # 15
parseInt("F", 16);                  # 15
parseInt("17", 8);                  # 15
parseInt("015", 10);                # 15
parseInt("15,123", 10);             # 15
parseInt("FXX123", 16);             # 15
parseInt("1111", 2);                # 15
parseInt("15 * 3", 10);             # 15
parseInt("15e2", 10);               # 15
parseInt("15px", 10);               # 15
parseInt("12", 13);                 # 15

# parses string to number. Spaces are allowed. Only the first number is returned:
parseFloat("10");                   # 10
parseFloat("10.33");                # 10.33
parseFloat("10 20 30");             # 10
parseFloat("10 years");             # 10
parseFloat("10,10 years");          # 10
parseFloat("years 10");             # NaN

# The Date() method returns the number of milliseconds since 1.1.1970.
Number(new Date("1970-01-01")) # It returns nothing as it is before the date
Number(new Date("1970-01-02")) # 86400000
Number(new Date("2017-09-30")) # 1506729600000

```

- Array: Creating it

```bash
const cars = ["Saab", "Volvo", "BMW"]; # use this
const cars = new Array("Saab", "Volvo", "BMW");

cars.toString()  # Saab,Volvo,BMW
cars.length   # Returns the number of elements

# Sorts the array ALPHABETICALLY USING ASIIC VALUE (NUMBERS ALSO )
const cars = ["Saab", 3, 25, 2, "Volvo", "BMW"];
cars.sort()    # [ 2, 25, 3, 'BMW', 'Saab', 'Volvo' ]
const cars = [3, 5, 2, 34, 0, 4];
cars.sort()    # [ 0, 2, 3, 34, 4, 5 ]
const cars = [3, 0, 4, , , , 1];
cars.sort()    # [ 0, 1, 3, 4, <3 empty items> ]

cars[6] = "Audi";  # Creates undefined "holes" in cars # NO UNDEFINED(MAYBE)

# You can have objects in an Array. You can have functions in an Array. You can have arrays in an Array:
myArray[0] = Date.now;
myArray[1] = myFunction;
myArray[2] = myCars;

# typeof operator in JavaScript returns "object" for arrays.
# SO 2 WAYS TO FIND IF IT'S ARRAY OR NOT
Array.isArray(cars); # returns true # To Know if it is array or not
cars instanceof Array # returns true
```

- Nested Arrays and Objects

```bash
const myObj = {
  name: "John",
  age: 30,
  cars: [
    {name:"Ford", models:["Fiesta", "Focus", "Mustang"]},
    {name:"BMW", models:["320", "X3", "X5"]},
    {name:"Fiat", models:["500", "Panda"]}
  ]
}
# of for array and in for object
for (let car of myObj.cars) {
  console.log(car.name);
  for (let model of car.models) {
    console.log(model);
  }
}
```

- Basic Array Methods

```bash
const fruits = ["Banana", "Orange", "Apple", "Mango"];
let size = fruits.length;

fruits.toString(); # Banana,Orange,Apple,Mango
fruits.join(" * "); # Banana * Orange * Apple * Mango

fruits.at(2); # allow negative index
fruits[2]; # negative not allowed

fruits.pop(); # removes and returns the last element
fruits.push("Kiwi");  # adds to the last element  and returns the new array length

fruits.shift(); # same as pop but for first element
fruits.unshift("Lemon"); # same as push but for first element

fruits[fruits.length] = "Kiwi"; # It will add to end of the array

# Don't do it
delete fruits[0]; # it leaves undefined holes in the array. # Use pop() or shift() instead.
# or use splice

const arr1 = ["Cecilie", "Lone"];
const arr2 = ["Emil", "Tobias", "Linus"];
const arr3 = ["Robin", "Morgan"];
const myChildren = arr1.concat(arr2); # add arr2 and arr1
const myChildren = arr1.concat(arr2, arr3); # add arr3, arr2 and arr1
const myChildren = arr1.concat("Peter"); #

const fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi"];
fruits.copyWithin(2, 0);
fruits.copyWithin(2, 0, 2);

# method overwrites the existing values + does not add items to the array + does not change the length of the array

const fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi", "grapes"];
fruits.copyWithin(2, 0); # [ 'Banana', 'Orange', 'Banana', 'Orange', 'Apple', 'Mango' ]
fruits.copyWithin(2, 0, 2) # [ 'Banana', 'Orange', 'Banana', 'Orange', 'Kiwi', 'grapes' ]

# Flattening is useful when you want to convert a multi-dimensional array into a one-dimensional array.
const myArr = [1, 2, [3, [4, 5, [6, 7]]]]; # array contains 3 sub-array
const newArr = myArr.flat(); # [ 1, 2, 3, [ 4, 5, [ 6, 7 ] ] ]
const newArr = myArr.flat(2); # [ 1, 2, 3, 4, 5, [ 6, 7 ] ]
const newArr = myArr.flat(3); # [ 1, 2, 3, 4, 5, 6, 7 ]
const newArr = myArr.flat(Infinity); # [ 1, 2, 3, 4, 5, 6, 7 ]


const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi"); # (start, deleteCount, ...items)
fruits.splice(3, 1); # here 1 item from 3rd position will be removed from the array
# Splice method modifies the original array and returns the deleted array.

const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
const citrus = fruits.slice(3); # [ 'Apple', 'Mango' ]
const citrus = fruits.slice(1, 3); # [ 'Orange', 'Lemon' ]
# Slice method doesn't mutate the original array but it returns the subset as a new array.

# All JavaScript objects have a toString() method.
```

- Array Find and Search Methods

```bash
const fruits = ["Apple", "Orange", "Apple", "Mango"];
let position = fruits.indexOf("Apple") + 1; # 1 # to get index of first apple + 1

let position = fruits.lastIndexOf("Apple") + 1; # 3 # to get index of last apple + 1

fruits.includes("Mango"); # is true

# find will return first element and filter will return all matched element
const numbers = [4, 9, 16, 25, 29];
let first = numbers.find((value, index, array) => {
  return value > 18;
});
let first = numbers.findIndex((value, index, array) => {
  return value > 18; # This will give first find index instead of the element value
});
let last = numbers.findLast((x) => x > 18); # give last value
let last = numbers.findLastIndex((x) => x > 18); # give last value index

```

- Array Sort Methods

```bash
# Alpabetic Sort
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort(); # Alphabetically like dictionary # THIS WILL ALTER THE ORIGINAL ARRAY
fruits.reverse(); # It will reverse the whole array
# So by combining both we can get array in descending order

#For descending Order # USE BUILD IN METHODS IF POSSIBLE (ABOVE AVOID THIS)
const sorted = fruits.sort((a, b) => b.localeCompare(a));

const sorted = fruits.toSorted(); # THIS WILL CREATE A NEW ARRAY WITHOUT ALTERING ORIGINAL
const sorted = fruits.toReversed(); # THIS WILL CREATE A NEW ARRAY WITHOUT ALTERING ORIGINAL

const points = [ 40, 100, 1, 5, 25, 10 ];
points.sort(function(a, b){return a - b}); # [ 1, 5, 10, 25, 40, 100 ] # numerical sort

const points = [ 40, 100, 1, 5, 25, 10 ];
points.sort(function(a, b){return b - a}); # [ 100, 40, 25, 10, 5, 1 ] # numerical sort
# Function used to determine the order of the elements. It is expected to return a negative value if the first argument is less than the second argument, zero if they're equal, and a positive value otherwise. If omitted, the elements are sorted in ascending, ASCII character order.

# SAME AS ABOVE BUT CUSTOM SORTING FUNCTION
points.sort((a, b) => {
  if (a < b) {
    return -1;
  } else if (a === b) {
    return 0;
  } else {
    return 1;
  }
};);

# Sorting objects based on property (YEAR)
const books = [
  { title: "Book A", year: 2010 },
  { title: "Book B", year: 2005 },
  { title: "Book C", year: 2018 },
];
const booksSortedByYearAsc = books.sort((a, b) => a.year - b.year);

# Sorting based on the content of the string
const names = ["Mike Smith", "Dr. Johnson", "John Doe", "Dr. Williams"];
names.sort((a, b) => {
  if (a.startsWith("Dr.") && !b.startsWith("Dr.")) {
    return -1; # Drs will come before
  } else if (!a.startsWith("Dr.") && b.startsWith("Dr.")) {
    return 1; # others will go back
  } else {
    return a.localeCompare(b); # Else sort alphabetically
  }
});

# Sorting Strings of Numbers and Letters
const items = ["b", "3", "a", "2", "c", "1"];

items.sort((a, b) => {
  const aIsNumber = !isNaN(a); # isNaN = is Not a Number
  const bIsNumber = !isNaN(b);

  if (aIsNumber && !bIsNumber) {
    return -1; # numbers should be sorted before letters (don't change)
  } else if (!aIsNumber && bIsNumber) {
    return 1; # letters should be sorted after numbers (change)
  } else if (aIsNumber && bIsNumber) {
    return a - b; # sort numbers numerically
  } else {
    return a.localeCompare(b); # sort letters alphabetically
  }
});

# Sorting an Array in Random Order
const points = [ 40, 100, 1, 5, 25, 10 ]; # ramdom will give number bw 0 to 1
# not accurate as it will favor some numbers over others.
points.sort(function(){return 0.5 - Math.random()});

# Find the Lowest (or Highest) Array Value
# 1. sort and then give first or last value for ascending and descending [AVOID AS IT WILL FIRST SORT ALL ARRAY THEN FIND IT]

# For min and max value in array [USE THIS OR write custom function for it]
function myArrayMin(arr) {
  return Math.min.apply(null, arr);
}
function myArrayMax(arr) {
  return Math.max.apply(null, arr);
}
```

- Array Iteration Methods

```bash

# ---------------> map, filter, reduce, foreach,..
# --> some(), every(), include(),
const arr = [1, 2, 3, 4, 5];

# forEach will not return the result after doing any operation init
# TAKES 3 ARGUMENTS map(value, index, array)
const for1 = arr.forEach((i) => i * 0); # ANSWERS ARE WRITTEN BELOW BUT FIRST GUESS THEM
const for2 = arr.forEach((i) => i * 1);
const for3 = arr.forEach((i) => i * 2);
const for4 = arr.forEach((i) => i % 2 === 0);

# map will return the result after doing any operation init "without changing original array"
# create a new array + will do operation on every element and then return that new element
# TAKES 3 ARGUMENTS map(value, index, array)
const map1 = arr.map((i) => i * 0);
const map2 = arr.map((i) => i * 1);
const map3 = arr.map((i) => i * 2);
const map4 = arr.map((i) => i % 2 === 0);

## This method returns all the elements of the array that satisfy the condition specified in the callback function.
# Filter will evaluate every element and will return same element if it returns true
# CHECK MAP VALUES IF TRUE THEN WILL RETURN THE ORIGINAL VALUE ELSE WON'T EG.. [ 0, 0, 0, 0, 0 ] THIS WILL RETURN [] (EMPTY ARRAY) 2.. [ false, true, false, true, false ] RETURN [  2, 4 ]
# TAKES 3 ARGUMENTS filter(value, index, array)
const fil1 = arr.filter((i) => i * 0);
const fil2 = arr.filter((i) => i * 1);
const fil3 = arr.filter((i) => i * 2);
const fil4 = arr.filter((i) => i % 2 === 0);

# Its a wrong way to write reduce -> BELOW GIVEN TRUE WAY TO WORK WITH REDUCE
# TAKES 4 ARGUMENTS reduce(previousValue/totalValue, currentValue, currentIndex, array)
const red1 = arr.reduce((i) => i * 0); # As all element will return false
const red2 = arr.reduce((i) => i * 1);
const red3 = arr.reduce((i) => i * 2); # every element will be double starting from 1st element
const red4 = arr.reduce((i) => i % 2 === 0); # A??? if %6 then why returning true

console.log({ for1 }); # undefined
console.log({ for2 }); # undefined
console.log({ for3 }); # undefined
console.log({ for4 }); # undefined
console.log({ map1 }); # [ 0, 0, 0, 0, 0 ]
console.log({ map2 }); # [ 1, 2, 3, 4, 5 ]
console.log({ map3 }); # [ 2, 4, 6, 8, 10 ]
console.log({ map4 }); # [ false, true, false, true, false ]
console.log({ fil1 }); # []
console.log({ fil2 }); # [ 1, 2, 3, 4, 5 ]
console.log({ fil3 }); # [ 1, 2, 3, 4, 5 ]
console.log({ fil4 }); # [ 2, 4 ] }
console.log({ red1 }); # 0 (0 * 0 * 0 * 0 ) [(1*0)*0*0*0] - as only one parameter(ie totalVal)
console.log({ red2 }); # 1 (1 * 1 * 1 * 1 ) [(1*1)*1*1*1] - as 1 is the first element
console.log({ red3 }); # 16 (2 * 2 * 2 * 2 ) - as if no initial value is provided (so 1 value)
console.log({ red4 }); # true - as (false(0) / 2 === 0); = true &-> (true / 2 === 0); = false

const arr4 = [1, 2, [3, [4, 5, [6, 7]]]] ; # array has 3 sub-arrays
console.log(arr4.flatMap((element) => element).flat(2)) ; # [1, 2, 3, 4, 5, 6, 7]

const numbers = [45, 4, 9, 16, 25];
# without initial value
let sum = numbers.reduce((total, value, index, array) => {
  return total + value; # 99 // [49,58,74,99]
});
# with initial value
let sum = numbers.reduce((total, value, index, array) => {
  return total + value; # 100 // [1,49,58,74,99]
}, 1);
# with initial value #==> reduceRight : IF 1ST VALUE IS STRING THEN THE VALUE IS DIFF
let sum = numbers.reduceRight((total, value, index, array) => {
  return total + value; # 100 # Same as right but it start from right
}, 1);
# To reverse an array without changing the orginal array
const originalArray = [1, 2, 3, 4, 5];
const newArray = originalArray.reduce((accumulator, value) => {
  return [value, ...accumulator];
}, []);
console.log(originalArray); // [1, 2, 3, 4, 5]
console.log(newArray); // [ 5, 4, 3, 2, 1]


# The every() method checks if all array values pass a test.
const numbers = [45, 4, 9, 16, 25];
let result = numbers.every((value, index, array) => {
  return value > 18;
  # false as all are not greater than 18(AS ALL VALUES ARE NOT RETURNING TRUE)
});

# The some() method checks if some array values pass a test.
const numbers = [45, 4, 9, 16, 25];
let result = numbers.some((value, index, array) => {
  return value > 18;
  # true as some are greater than 18(AS SOME VALUES ARE RETURNING TRUE)
});
});

# returns an Array object from any object with a length property or any iterable object
Array.from("ABCD"); # [ 'A', 'B', 'C', 'D' ]

# You can map the array values without using the map method by just using the from method of Array.
const countries = [
  { name: "India", capital: "Delhi" },
  { name: "US", capital: "Washington" },
  { name: "Russia", capital: "Moscow" },
  { name: "Singapore", capital: "Singapore" },
  { name: "China", capital: "Beijing" },
  { name: "France", capital: "Paris" },
];
const cityNames = Array.from(countries, ({ capital }) => capital);
console.log(cityNames); # ['Delhi, 'Washington', 'Moscow', 'Singapore', 'Beijing', 'Paris']


# The Array.keys() method returns an Array Iterator object with the keys of an array.
# The entries() method returns an Array Iterator object with key/value pairs:
const fruits = ["Banana", "Orange", "Apple", "Mango"];
for (let x of fruits) {
  console.log(x); # Banana, Orange, Apple, Mango
}

console.log(fruits.keys()); #Object [Array Iterator] {}

for (let x of fruits.keys()) {
  console.log(x); # 0,1,2,3
}

console.log(fruits.values()); #Object [Array Iterator] {}

for (let x of fruits.values()) {
  console.log(x); # Banana, Orange, Apple, Mango
}

for (let x of fruits.entries()) {
  console.log(x); # [ 0, 'Banana' ],[ 1, 'Orange' ],[ 2, 'Apple' ],[ 3, 'Mango' ]
}

# JS Array Spread (...) operator expands an iterable (like an array) into more elements:
const q1 = ["Jan", "Feb", "Mar"];
const q2 = ["Apr", "May", "Jun"];
const q3 = ["Jul", "Aug", "Sep"];
const q4 = ["Oct", "Nov", "Dec"];
const year = [ ...q1, ...q2, ...q3, ...q4];
# ['Jan', 'Feb', 'Mar','Apr', 'May', 'Jun','Jul', 'Aug', 'Sep','Oct', 'Nov', 'May']
```

- JavaScript Date Objects

```bash
# Date objects are static. The "clock" is not "running".
# The computer clock is ticking, date objects are not.

# There are 9 ways to create a new date object:
new Date()
new Date(date string) # string ("12-12-12")
new Date(year,month) # number (2000,12)
new Date(year,month,day)
new Date(year,month,day,hours)
new Date(year,month,day,hours,minutes)
new Date(year,month,day,hours,minutes,seconds)
new Date(year,month,day,hours,minutes,seconds,ms)
new Date(milliseconds) # number (290498502)

#(YYYY-MM-DD)
const d = new Date(); # give current date #Sat Jun 22 2024 15:54:58 GMT+0530 (IST)
const d = new Date("2015-03-25"); # give this date # Fri Mar 25 2022 05:30:00 GMT+0530 (IST)
const d = new Date("03/25/2015"); # adds 0 in tens else may cause errors
#const d = new Date("25-03-2015"); # ERROR => THIS CAN CAUSE ERROR
const d = new Date("2015-03");
const d = new Date("2015");
const d = new Date("October 13, 2014 11:13:00");
# Long dates are most often written with a "MMM DD YYYY" syntax like this:
# And, month can be written in full (January), or abbreviated (Jan):
# Commas are ignored. Names are case insensitive:
const d = new Date("25 Jan 2015"); # Month and day can be in any order:
const d = new Date("Jan 25 2015");
const d = new Date("January 25 2015");
const d = new Date("JANUARY, 25, 2015");

# You cannot omit month. If you supply write only one parameter it will be treated as milliseconds.
const d = new Date(2018); # THIS WILL BE TREATED AS MILISECOND
const d = new Date(2018, 11);
const d = new Date(2018, 11, 24);
const d = new Date(2018, 11, 24, 10);
const d = new Date(2018, 11, 24, 10, 33);
const d = new Date(2018, 11, 24, 10, 33, 30);
const d = new Date(2018, 11, 24, 10, 33, 30, 0);

# JavaScript counts months from 0 to 11:
# Specifying a month higher than 11, will not result in an error but add the overflow to the next year:
const d = new Date(2018, 15, 24, 10, 33, 30); # Fri Dec 24 1909
const d = new Date(2019, 3, 24, 10, 33, 30); # Fri Dec 24 1909

# Specifying a day higher than max, will not result in an error but add the overflow to the next month:

# One and two digit years will be interpreted as 19xx:
const d = new Date(99, 11, 24); # Fri Dec 24 1999 00:00:00 GMT+0530 (India Standard Time)
const d = new Date(9, 11, 24); # Fri Dec 24 1909 00:00:00 GMT+0530 (India Standard Time)

# JavaScript stores dates as number of milliseconds since January 01, 1970.
# One day (24 hours) is 86 400 000 milliseconds.

const d = new Date(0); # 1970-01-01T00:00:00.000Z
const d = new Date(24 * 60 * 60 * 1000); # 1 day added # 1970-01-02T00:00:00.000Z
const d = new Date(86400000); # same as above  # 1 day added
# To go back a day
const d = new Date(-86400000); # Go back one day # 1969-12-31T00:00:00.000Z

# Displaying Dates
new Date().toString() # Sat Jun 22 2024 16:47:57 GMT+0530 (India Standard Time)
new Date().toDateString() # Sat Jun 22 2024
new Date().toUTCString() # Sat, 22 Jun 2024 11:19:41 GMT
new Date().toISOString() # 2024-06-22T11:19:41.416Z
new Date().toLocaleDateString() # 6/22/2024
new Date().toLocaleTimeString() # 4:51:29 PM
# REVISE
let msec = Date.parse("March 21, 2012"); # 1332268200000 # To convert date to millisecond
let date = new Date(86400000); # To convert millisecond into date
```

- Date Get Methods

```bash
const d = new Date();
d.getFullYear(); # 2024
d.getMonth()+1; # 6 (0-11) # can create an array and use this to get month
d.getDate(); # 22 (1-31)
d.getHours(); # 17 (0-23)
d.getMinutes(); # 19 (0-59)
d.getSeconds(); # 55 (0-59)
d.getMilliseconds(); #  493 (0-999)
d.getDay(); # 6 (0-6) # starting from sun (can create an array and use this to get day)
d.getTime(); # 1719057456184 # It returns milliseconds since January 1, 1970
Date.now(); # 1719057456184 # It returns milliseconds since January 1, 1970 [SAME AS ABOVE]

new Date("1969-01-01").getTime() # -31536000000
new Date("1970-01-01").getTime() # 0
new Date("1971-01-01").getTime() # 31536000000

d.getTimezoneOffset(); # -330 (-5.5 hrs) # difference (in min) between local time an UTC time

```

- JavaScript Set Date Methods (To set (change) the date value)

```bash
const d = new Date();
d.setFullYear(2020);
d.setFullYear(2020, 11, 3);
d.setMonth(11); # month changed to dec (0-11)
d.setDate(15); # (1-31)
d.setDate( d.getDate() + 50);  # date is 50 day ahead
d.setHours(22); #  (0-23)
d.setMinutes(30); # (0-59)
d.setSeconds(30); # (0-59)

const today = new Date();
const someday = new Date("2222-05-05");
someday > today # true # You can compate the dates directly

```

- JavaScript Math Object
- Unlike other objects, the Math object has no constructor. The Math object is static.
- All methods and properties can be used without creating a Math object first.

```bash

- Math Properties (Constants)

# JavaScript provides 8 mathematical constants that can be accessed as Math properties:
Math.E        # returns Euler's number
Math.PI       # returns PI
Math.SQRT2    # returns the square root of 2
Math.SQRT1_2  # returns the square root of 1/2
Math.LN2      # returns the natural logarithm of 2
Math.LN10     # returns the natural logarithm of 10
Math.LOG2E    # returns base 2 logarithm of E
Math.LOG10E   # returns base 10 logarithm of E

- Math Methods

# Math.round(x) returns the nearest integer
# Math.round => round to the nearest integer(9.4999=9;9.50=10)
Math.round(4.6); # 5
Math.round(4.5); # 5
Math.round(4.4); # 4

# Math.ceil(x) returns the value of x rounded up to its nearest integer
# Math.ceil => If have integer then give next number(56.999=57;56.0001=57) // [floor+1]
Math.ceil(-4.1); # -4
Math.ceil(-4.9); # -4
Math.ceil(4.1); # 5
Math.ceil(4.9); # 5

# Math.floor(x) returns the value of x rounded down to its nearest integer
# Math.floor => remove the float points and convert into integer(56.999=56;56.0001=56)
Math.floor(-4.1); # -5
Math.floor(-4.9); # -5
Math.floor(4.1); # 4
Math.floor(4.9); # 4

# Math.trunc(x) returns the integer part of x
Math.trunc(-4.1); # -4
Math.trunc(-4.9); # -4
Math.trunc(4.1); # 4
Math.trunc(4.9); # 4

# Math.sign(x) returns if x is negative, null or positive
Math.sign(-4.312) # -1
Math.sign(0) # 0
Math.sign(434.312) # 1

Math.pow(8, 2); # 64 # Math.pow(x, y) returns the value of x to the power of y
Math.sqrt(64); # 8 # Math.sqrt(x) returns the square root of x
Math.abs(-4.7); # 4.7 # Math.abs(x) returns the absolute (positive) value of x
Math.sin(x)
Math.cos(x)

# Math.min() and Math.max() used to find the lowest or highest value in a list of arguments
Math.min( 0, 150, 30, 20, -8, -200); # -200
Math.max( 0, 150, 30, 20, -8, -200); # 150

Math.log(1); # 0 # log1 is always "0"
Math.log(8); # 2.0794415416798357
Math.log2(8); # 3
Math.log10(1000); # 3

Math.random(); # 0.3083259775841265 # random number between 0 (inclusive), and 1 (exclusive)
Math.floor( Math.random() * 10 ); # Returns a random integer from 0 to 9
Math.floor( Math.random() * 10) + 1; # Returns a random integer from 1 to 10

function getRndInteger(min, max) {
  return Math.floor(Math.random() * (max - min + 1) ) + min;
}
getRndInteger(5, 10) # get random number from 5 to 10 [5,6,7,8,9,10]

```

- JavaScript Booleans

```bash

# Values that return true
let x = 100;
let x = 3.14;
let x = -15;
let x = "Hello";
let x = "false";
let x = 7 + 1 + 3.14;
Boolean(x); # return true

# Values that return false
let x = 0;
let x = -0;
let x = "";
let x; # ie. undefined
let x = null;
let x = false;
let x = 10 / "Hallo"; # ie NaN
Boolean(x); # return false

# both are not equal by type(===) only equal by value(==)
let x = false;
let y = new Boolean(false); # Do not create Boolean objects.

# Comparison Operators

let x = 5;

x == 8   # false # equal to (equal value)
x == 5   # true
x == "5" # true

x === 5	  # true # equal value and equal type
x === "5" #	false

x != 8	# true # not equal

x !== 5	  # false # not equal value or not equal type
x !== "5" # true
x !== 8	  # true

x > 8	# false # greater than
x < 8	# true # less than
x >= 8	# false # greater than or equal to
x <= 8	# true # less than or equal to

let x = 6, y = 3;

(x < 10 && y > 1) # true # and
(x == 5 || y == 5) # false # or
!(x == y) # true # not

# Conditional (Ternary) Operator
# variablename = (condition) ? value1:value2

# When comparing two strings, "2" will be greater than "12", because (alphabetically) 1 is less than 2.
"2" < "12" # false
2 < 12 # true

# The ?? operator returns the first argument if it is not nullish (null or undefined).
null ?? undefined ?? 0 ?? text # 0 will be printed

# The Optional Chaining Operator (?.)
car?.name # If value is undefined it won't throw an error

10 == [[[[[10]]]]]                                        # returns true
# 10 === Number([10].valueOf().toString()); // 10

```

- Conditional Statements (if, if-else, if-else if, switch)
- The JavaScript Switch Statement

```bash
# If not writing break statement then if case matched, it will execute all cases below it until break is found or block is completed
# You can write default case anywhere in the block, BUT IF IT'S NOT AT LAST THEN WRITE BREAK AFTER IT.

switch (new Date().getDay()) {
  case 6:
    text = "Today is Saturday";
    break;
  case 0:
    text = "Today is Sunday";
    break;
  default:
    text = "Looking forward to the Weekend"; # NO BREAK STATEMENT AFTER IT
}

switch (new Date().getDay()) {
  default:
    text = "Looking forward to the Weekend";
    break; # NEED TO WRITE BREAK STATEMENT
  case 6:
    text = "Today is Saturday";
    break;
  case 0:
    text = "Today is Sunday";
}

# Common Code Blocks
switch (new Date().getDay()) {
  case 4:
  case 5:
    text = "Soon it is Weekend";
    break;
  case 0:
  case 6:
    text = "It is Weekend";
    break;
  default:
    text = "Looking forward to the Weekend";
}

# If multiple cases matches a case value, the first case is selected.
# If no matching cases are found, the program continues to the default label.
# If no default label is found, the program continues to the statement(s) after the switch.

# Switch cases use strict comparison (===).
let x = "0";
switch (x) {
  case 0:
    text = "Off";
    break;
  case 1:
    text = "On";
    break;
  default:
    text = "No value found"; # This will be executed
}
```

- Different Kinds of Loops

```bash
# for - loops through a block of code a number of times
# for/in - loops through the properties of an object
# for/of - loops through the values of an iterable object
# while - loops through a block of code while a specified condition is true
# do/while - Same as while but will run the code atleast ones

# Expression 1 [OPTIONAL] - (let i = 0;)

# Normally you will use expression 1 to initialize the variable used in the loop (let i = 0).
# You can initiate many values in expression 1 (separated by comma)
for (let i = 0, len = cars.length, text = ""; i < len; i++) {
  text += cars[i] + "<br>";
} # HERE LEN IS NOT DEFINED EARLY AS LEN IS NOT REQUIRED OUTSIDE IF THE BLOCK, WE DON'T WRITE DIRECTLY I < CARS.LENGTH AS IT WILL CALCULATE LEN ON EVERY ITERATION.S

# you can omit expression 1 (like when your values are set before the loop starts):

# Expression 2 [OPTIONAL] - (i < len;)

# Often expression 2 is used to evaluate the condition of the initial variable
# If expression 2 returns true, the loop will start over again. If it returns false, the loop will end.
# If you omit expression 2, you must provide a break inside the loop. Otherwise the loop will never end.

# Expression 3 [OPTIONAL] - (i++)

# Often expression 3 increments the value of the initial variable.
# Expression 3 can do anything like negative increment (i--), positive increment (i = i + 15), or anything else.
# Expression 3 can also be omitted (like when you increment your values inside the loop):

# FOR LOOP WITHOUT ANY EXPRESSION (1, 2, 3)
const cars = ["BMW", "Volvo", "Saab", "Ford"];
let i = 0;
let len = cars.length;
let text = "";
for (;;) {
  text += cars[i] + " ";
  console.log(text);
  i++;
  if (!(i < len)) break;
}

# FLOW: EXPRESS -> 1,2,CODE,3,2,CODE,3,2,CODE,3,2,....
# 1: INITIALIZE, 2: CHECK, 3: INCRESE

```

- The For In Loop in JS
- THE JAVASCRIPT FOR IN STATEMENT LOOPS THROUGH THE PROPERTIES OF AN OBJECT

```bash

# THE JAVASCRIPT FOR IN STATEMENT LOOPS THROUGH THE PROPERTIES OF AN OBJECT

# Each iteration returns the value of the key ie. person[x], cars[x]
const person = { fname: "John", lname: "Doe", age: 25 };
let text1 = "";
for (let x in person) {
  text1 += person[x] + " "; # John Doe 25
}

# DO NOT USE FOR IN OVER AN ARRAY IF THE INDEX ORDER IS IMPORTANT.
# THE INDEX ORDER IS IMPLEMENTATION-DEPENDENT, AND ARRAY VALUES MAY NOT BE ACCESSED IN THE ORDER YOU EXPECT.
# USE FOR LOOP, FOR OF LOOP, OR ARRAY.FOREACH() WHEN THE ORDER IS IMPORTANT.

# AVOID ARRAY for FOR-IN LOOP [USE FOR-OF LOOP]
const cars = ["BMW", "Volvo", "Saab", "Ford"];
let text2 = "";
for (let x in cars) {
  text2 += cars[x] + " "; # BMW Volvo Saab Ford
}

```

- The For Of Loop in JS
- THE JAVASCRIPT FOR OF STATEMENT LOOPS THROUGH THE VALUES OF AN ITERABLE OBJECT.
- It lets you loop over iterable data structures such as Arrays, Strings, Maps, NodeLists, and more

```bash

const cars = ["BMW", "Volvo", "Mini"];
let text = "";
for (let x of cars) {
  text += x + " "; # BMW Volvo Mini
}
const cars = "ABCDEFGH";
let text = "";
for (let x of cars) {
  text += x + " "; # A B C D E F G H
}

```

- While and do-while loop

```bash
while (i < 10) {
  text += "The number is " + i;
  i++;
}

do {
  text += "The number is " + i;
  i++;
}
while (i < 10);

# Here when cars[i] will become undefined then while loop will be false and removed
const cars = ["BMW", "Volvo", "Saab", "Ford"];
let i = 0;
let text = "";

# YOU CAN USE THIS TRICK "cars[i]" IN THE FOR LOOP ALSO
while (cars[i]) {
  text += cars[i];
  i++;
}
```

- JavaScript Break and Continue

- The break statement "jumps out" of a loop.
- The continue statement "jumps over" one iteration in the loop.

-

- Label Statement

- The Label Statement is used with the break and continue statements and serves to identify the statement to which the break and continue statements apply.

```bash
# Without the use of a labeled statement the break statement can only break out of a loop or a switch statement. Using a labeled statement allows break to jump out of any code block.

foo: { # without foo the break statement will give an error
  console.log("This prints:");
  break foo;
  console.log("This will never be printed.");
}
console.log("Because execution jumps to here!")


# without labeled statement, when j==i inner loop jumps to next iteration
for (let i = 0; i < 3; i++) {
  console.log("i=" + i);
  for (let j = 0; j < 3; j++) {
    if (j === i) {
      continue;
    }
    console.log("j=" + j);
  }
} # i=0, j=1, j=2, i=1, j=0, j=2, i=2, j=0, j=1, (note j=0, j=2, j=3 is missing)

# using a labeled statement we can jump to the outer (i) loop instead
outer: for (let i = 0; i < 3; i++) {
  console.log("i=" + i);
  for (let j = 0; j < 3; j++) {
    if (j === i) {
      continue outer;
    }
    console.log("j=" + j);
  }
} # i=0, i=1, j=0, i=2, j=0, j=1, (note j=0, j=2, j=3, j=1, j=2, j=2, is missing)

# EXAMPLE
# --> WILL GIVE ERROR
const arr = [1, 2, 3, 4, 5];
arr.forEach((val) => {
  if (val % 2 === 0) {
     break; # ERROR AS BREAK CAN ONLY WORKS INSIDE A LOOP AND IN FOREACH IT'S INSIDE FUNCTION
  }
  console.log(val);
});

# --> WILL WORK
for (let i = 0, len = arr.length; i < len; i++) {
  if (arr[i] % 2 === 0) {
    break; # THIS WILL WORK AS BREAK IS INSIDE A LOOP
  }
  console.log(arr[i]);
}

```

- JavaScript Iterables

- Iterables are iterable objects (like Arrays).
- Iterables can be iterated over with for..of loops

- An object becomes an iterator when it implements a next() method.
- The next() method must return an object with two properties:
  - value (the next value) - (Can be omitted if done is true)
  - done (true or false) - (true if the iterator has completed false if the iterator has produced a new value)
- Technically, iterables must implement the Symbol.iterator method.

```bash

# Create an Object
myNumbers = {};

# Make it Iterable
myNumbers[Symbol.iterator] = function() {
  let n = 0;
  done = false;
  return {
    # next() method is returning a object with 2 properties(value and done)
    next() {
      n += 10;
      if (n == 100) {done = true}
      return {value:n, done:done};
    }
  };
}
# Now you can use for..of

```

- JavaScript Sets
- unique values + only occur once + can be of any type + primitive values or objects.

```bash
# Create a Set --- Pass an array to the new Set() constructor:
const letters = new Set(["a","b","c"]);

# Add Values to the Set
letters.add("c"); # This won't be added as already present
letters.add("C"); # This will be added as capital C
letters.add("d"); # added
const val = "e";
letters.add(val); # added
console.log(letters); # Set(6) { 'a', 'b', 'c', 'C', 'd', 'e' }
# Listing Set Elements
for (const x of letters) {
  console.log(x); # 'a', 'b', 'c', 'C', 'd', 'e'
}

typeof letters;          # Returns object
letters instanceof Set;  # Returns true

letters.has("d"); # true # return true if it exists in the set

letters.forEach((v) => console.log(v)); #forEach method

# The values() method returns an Iterator object with the values in a Set
for (const x of letters.values()) {
  console.log(x); # 'a', 'b', 'c', 'C', 'd', 'e' # ?????? Looking same as above
}

# The keys() method returns an Iterator object with the values in a Set - [SAME AS ABOVE]
# A Set has no keys, so keys() returns the same as values() To makes it compatible with Maps.
for (const x of letters.keys()) {
  console.log(x); # 'a', 'b', 'c', 'C', 'd', 'e' # SAME AS ABOVE
}

# The entries() method returns an Iterator with [value,value] pairs from a Set.
# The entries() method is supposed to return a [key,value] pair from an object.
# A Set has no keys, so the entries() method returns [value,value].
# This makes Sets compatible with Maps.
for (const x of letters.entries()) {
  console.log(x);
} # [ 'a', 'a' ], [ 'b', 'b' ],...,[ 'e', 'e' ]
```

- JavaScript Maps

- A Map holds key-value pairs where the keys can be any datatype.
- A Map remembers the original insertion order of the keys. [WHICH VALUE INSERTED 1ST]
- Keys are unique ?[YES]
- Maps accept any data type as a key, and do not allow duplicate key values.
- If duplicate key then the latest/last value is considered (in both map and object)

  Objects are similar to Maps in that both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key. Due to this reason, Objects have been used as Maps historically. But there are important differences that make using a Map preferable in certain cases:

      - The keys of an Object can be Strings and Symbols, whereas they can be any value for a Map, including functions, objects, and any primitive type.
      - The keys in a Map are ordered while keys added to Object are not. Thus, when iterating over it, a Map object returns keys in the order of insertion.
      - You can get the size of a Map easily with the size property, while the number of properties in an Object must be determined manually.
      - A Map is an iterable and can thus be directly iterated, whereas iterating over an Object requires obtaining its keys in some fashion and iterating over them.
      - An Object has a prototype, so there are default keys in an object that could collide with your keys if you're not careful. As of ES5 this can be bypassed by creating an object(which can be called a map) using Object.create(null), but this practice is seldom done.
      - A Map may perform better in scenarios involving frequent addition and removal of key pairs.

```bash
# Create a Map
const fruits = new Map([ ["apples", 500],["bananas", 300],["oranges", 200] ]);

# You can add elements to a Map with the set() method
fruits.set("mangos", 800);
# change existing Map values using set() method
fruits.set("apples", 300);
# gets the value of a key in a Map using get() method
fruits.get("apples");    # Returns 500

typeof fruits; # Returns object
fruits instanceof Map; # Returns true

fruits.size; # 4 # return the total size of map object

fruits.clear(); # The clear() method removes all the elements from a map

fruits.delete("apples"); # The delete() method removes a map element

fruits.has("apples"); # true if exists in fruits map else false

# The forEach() method invokes a callback for each key/value pair in a map
# forEach(value,key,array) (500, apples, { 'apples' => 500, 'bananas' => 300, 'oranges' => 200 })
fruits.forEach((x, y) => console.log(x, y)); # x is values and y is keys

for (const x of fruits) {
  console.log(x); # [ 'apples', 300 ], [ 'bananas', 300 ],..
}

for (const x of fruits.keys()) {
  console.log(x); # apples, bananas,..
}

for (const x of fruits.values()) {
  console.log(x); # 400,300,200,..
}

for (const x of fruits.entries()) {
  console.log(x); # [ 'apples', 300 ], [ 'bananas', 300 ],..
}

# Objects as Keys -[CREATE A MAP FROM OBJECT]- THEN YOU CAN'T USE .GET METHOD ON IT

// Create Objects
const apples = {name: 'Apples'};
const bananas = {name: 'Bananas'};
const oranges = {name: 'Oranges'};

// Create a Map
const fruits = new Map();

// Add new Elements to the Map
fruits.set(apples, 500);
fruits.set(bananas, 300);
fruits.set(oranges, 200);

# object is key
for (const x of fruits.entries()) {
  console.log(x); # [ { name: 'Apples' }, 500 ],[ { name: 'Bananas' }, 300 ],..
}

# cannot get if you are converting from object
fruits.get("apples");             # Returns undefined
fruits.get({ name: "Apples" });   # Returns undefined
# REVISE
```

- The typeof Operator
- The typeof operator returns the data type of a JavaScript variable.
- JavaScript has 7 primitive data types and one complex data type: object

```bash
typeof "John"                                 # Returns string
typeof ("John"+"Doe")                         # Returns string
typeof 3.14                                   # Returns number
typeof 33                                     # Returns number
typeof (33 + 66)                              # Returns number
typeof true                                   # Returns boolean
typeof false                                  # Returns boolean
typeof 1234n                                  # Returns bigint
typeof Symbol()                               # Returns symbol
typeof x                                      # Returns undefined
typeof null                                   # Returns object # null is a primitive value, but returns "object".

# All other complex types like arrays, functions, sets, & maps are different types of objects.
# The typeof operator returns only two types: > object and > function
typeof {name:'John'}                          # Returns object
typeof [1,2,3,4]                              # Returns object
typeof new Map()                              # Returns object
typeof new Set()                              # Returns object
typeof function (){}                          # Returns function

# How to Recognize an Array
const fruits = ["apples", "bananas", "oranges"];
Array.isArray(fruits); # true
arr instanceof Array # true

------- # The instanceof Operator

# The instanceof operator returns true if an object is an instance of a specified object type
# YOU CANNOT GET INSTANCEOF NULL AND UNDEFINED AS THEY ARE NOT OBJECT
const car = null;
car instanceof null; # ERROR
const car = undefined;
car instanceof undefined; # ERROR

# Create a Date
const time = new Date();
(time instanceof Date); # returns true

# Create an Array
const fruits = ["apples", "bananas", "oranges"];
(fruits instanceof Array); # returns true

# Create a Map
const fruits = new Map([
  ["apples", 500],
  ["bananas", 300],
  ["oranges", 200]
]);
(fruits instanceof Map); # returns true

# Create a Set
const fruits = new Set(["apples", "bananas", "oranges"]);
(fruits instanceof Set); # returns true

----- # Undefined Variables

typeof car; # undefined # without defining any variable it will be undefined

let car;
typeof car; # undefined # if defined but not given any value then also undefined

let car = undefined;
typeof car; # undefined # if value is undefined then also type will be undefined

----------- # Null
# You can empty an object by setting it to null. The data type of null is an object.
let car = null;
typeof car; # object

# Create an Object
let person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};

person = null; # Now value is null, but type is still an object
person = undefined; # Now both value and type is undefined

typeof undefined      # undefined
typeof null           # object # and not null
# REVISE
null === undefined    # false
null == undefined     # true OOOOOOOOO BOTH ARE EQUAL HERE OOOOOOOOOO

---------------------- TLDR

typeof "John"                                 # Returns "string"
typeof ("John"+"Doe")                         # Returns "string"
typeof 3.14                                   # Returns "number"
typeof (33 + 66)                              # Returns "number"
typeof NaN                                    # Returns "number" # NaN is a number
typeof 1234n                                  # Returns "bigint"
typeof true                                   # Returns "boolean"
typeof false                                  # Returns "boolean"
typeof {name:'John'}                          # Returns "object"
typeof [1,2,3,4]                              # Returns "object"
typeof {}                                     # Returns "object"
typeof []                                     # Returns "object"
typeof new Object()                           # Returns "object"
typeof new Array()                            # Returns "object"
typeof new Date()                             # Returns "object"
typeof new Set()                              # Returns "object"
typeof new Map()                              # Returns "object"
typeof function () {}                         # Returns "function"
typeof x                                      # Returns "undefined"
typeof null                                   # Returns "object" # It's an object and not null
```

- JavaScript Type Conversion

```bash
1.----- Converting Strings to Numbers
- Number(), parseFloat(), parseInt(), +

Number("3.14")                            # 3.14
Number(Math.PI)                           # 3.141592653589793
Number("    ")                            # 0
Number("")                                # 0
Number("  10  ")                          # 10
Number("99 88")                           # NaN # it's NaN and not 99 # use parseInt()
Number("John")                            # NaN

+"3.14"                                   # 3.14
+Math.PI                                  # 3.141592653589793
+"    "                                   # 0
+""                                       # 0
+"  10  "                                 # 10
+"99 88"                                  # NaN # it's NaN and not 99 # use parseInt() maybe
+"John"                                   # NaN

2.----- Converting Numbers to Strings

let x = 43;
String(x);
String(123);
String(100 + 23);
# same as above
x.toString();
(123).toString();
(100 + 23).toString();

3.----- Converting Dates to Numbers

d = new Date();
Number(d)    # returns 1404568027739
d.getTime()  # returns 1404568027739

4.----- Converting Dates to Strings

String(Date())
Date().toString()
# get methods also convert dates into strings (eg. getFullYear(), getDay(),..)

5.----- Converting Booleans to Numbers

Number(false)                               # returns 0
Number(true)                                # returns 1

6.----- Converting Booleans to Strings

String(false)                               # returns "false"
String(true)                                # returns "true"
String(null)                                # returns "null"
false.toString()                            # returns "false"
true.toString()                             # returns "true"

7.----- Automatic Type Conversion

5 + null                  # returns 5         # because null is converted to 0
"5" + null                # returns "5null"   # because null is converted to "null"
"b" + 2                   # returns "b2"      # because b is converted to "b"
"5" + 2                   # returns "52"      # because 2 is converted to "2"
"5" - 2                   # returns 3         # because "5" is converted to 5
"5" * "2"                 # returns 10        # because "5" and "2" are converted to 5 and 2
"5" * "a"                 # returns NaN       # because alphabets can't be converted to number

8.----- Automatic String Conversion

# When tries to get an output to DOM (document.getElementById("demo").innerHTML = myVar;)

myVar = {name:"Fjohn"}  // toString converts to "[object Object]"
myVar = [1,2,3,4]       // toString converts to "1,2,3,4"
myVar = new Date()      // toString converts to "Fri Jul 18 2014 09:08:55 GMT+0200"
# Numbers and booleans are also converted, but they are not very visible
myVar = 123             // toString converts to "123"
myVar = true            // toString converts to "true"
myVar = false           // toString converts to "false"

myVar.toString()

# REVISE
9.----- JavaScript Type Conversion Table
---- https://www.w3schools.com/js/js_type_conversion.asp ---> Go and check [for full table]
# TLDR
console.log(Boolean("0"));                                     # true
console.log(Boolean(0));                                       # false
console.log(Boolean(NaN));                                     # false
console.log(Boolean("NaN"));                                   # true
console.log(Boolean(Infinity));                                # true
console.log(Boolean(""));                                      # false # empty string is false
console.log(Number(""));                                       # 0
console.log(Boolean([]));                                      # true # empty array is true
console.log(Boolean({}));                                      # true # empty object is true
console.log(Number([]));                                       # 0
console.log(Number({}));                                       # NaN
console.log(String([]));                                       # ""
console.log(String({}));                                       # "[object Object]"
console.log(Number([20]));                                     # 20
console.log(Number(null));                                     # 0 # null is 0
console.log(Number(undefined));                                # NaN # undefined is NaN
console.log(Boolean(null));                                    # false
console.log(Boolean(undefined));                               # false
console.log(isNaN(1));                                         # false
console.log(isNaN("1"));                                       # false
console.log(isNaN("1a"));                                      # true
console.log(isNaN("1 3"));                                     # true
# NEW ADDED
console.log("0" == false);                                     # true
console.log([[[[0]]]] == false); # ([[0]].valueOf().toString())# true
console.log(0 == false);                                       # true
console.log(0 === false);                                      # false
console.log("0" === false);                                    # false
console.log(NaN === NaN);

# The variables such as objects, arrays and functions comes under pass by reference
# so comparing them will always returns false
{} === {}, [] === []
```

- JavaScript Destructuring
- Destructuring does not change the original object.

```bash
# Destructuring can be used with any iterables.

# The order of the properties does not matter
# For potentially missing properties we can set default values = [ie. IF UNDEFINED]
1. -------- Object destructuring
# Create an Object
const person = {
  firstName: "John",
  lastName: "Doe",
  working: null,
  age: undefined,
  city: "Ahmedabad",
};

# Destructuring
let { lastName, firstName = "Mahesh", country = "US", working= "Soon", age = 10, city:town } = person;

console.log(firstName);                         # John # Not Mahesh as firstName value exists
console.log(lastName);                          # Doe
console.log(country);                           # US # As country value doesn't exists
console.log(working);                           # null as null is provided
console.log(age);                               # 10 # if undefined then default value
console.log(city);                              # This will through an error
console.log(town);                              # Ahmedabad # as now the name has been changed

# DESTRUCTURE NESTED OBJECTS
const vehicleOne = {
  brand: 'Ford',
  model: 'Mustang',
  type: 'car',
  year: 2021,
  color: 'red',
  registration: {
    city: 'Houston',
    state: 'Texas',
    country: 'USA'
  }
}
myVehicle(vehicleOne)

function myVehicle({ model, registration: { state } }) {
  const message = 'My ' + model + ' is registered in ' + state + '.';
}

2. -------- String destructuring

# Create a String
let names = "W3Schools";

# Destructuring
let [ a1, z9, a3, a4, a5] = names;
console.log( a1, z9, a3); # You can use any name

3. -------- Array destructuring

# Create an Array
const fruits = ["Bananas", "Oranges", "Apples", "Mangos"];

# Destructuring
let [fruit1, fruit2] = fruits; # Bananas Oranges

# We can skip array values using two or more commas
let [fruit1,,,fruit2] = fruits; # Bananas Mangos

# We can pick up values from specific index locations of an array
let { [0]:fruit1 ,[2]:fruit2 } = fruits; # Bananas Apples # USE CURLY BRACKETS FOR THIS

----- The Rest Property # can also be used in objects (may be for all iterables)

const numbers = [10, 20, 30, 40];
const [ a, b, ...rest ] = numbers;
console.log( a, rest ); # 10 [ 30, 40 ]

4. ------- Destructuring Maps

# Create a Map
const fruits = new Map([
  ["apples", 500],
  ["bananas", 300],
  ["oranges", 200],
]);

# Destructing
for (const [myKey, myValue] of fruits) {
  console.log(myKey, myValue); # apples 500, bananas 300, oranges 200
}

5. ------- Swapping JavaScript Variables

let firstName = "John";
let lastName = "Doe";

# Destructing in variables
[firstName, lastName] = [lastName, firstName];
console.log( firstName, lastName); # Doe John

# BELOW CAN BE DONE BY REGULAR WAYS
[firstName] = [lastName]; #lastName is changed to John (value of first name)
firstName = lastName; # Same as above
console.log( firstName, lastName); # John John
[firstName] = ["myName"]; # firstName changed to myName --->>> Can directly change this
firstName = "myName"; # Same as above
console.log( firstName, lastName); # myName John

```

- JavaScript Bitwise Operators ( NOT GOING DEEP IN THIS TOPIC)

```bash
--------- FOR MORE INFO # https://www.w3schools.com/js/js_bitwise.asp

&	AND
# Sets each bit to 1 if both bits are 1
|	OR
# Sets each bit to 1 if one of two bits is 1
^	XOR
# Sets each bit to 1 if only one of two bits is 1
~	NOT
# Inverts all the bits
>>	Signed right shift
# Shifts right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off
>>>	Zero fill right shift
# Shifts right by pushing zeros in from the left, and let the rightmost bits fall off
<<	Zero fill left shift
# Shifts left by pushing zeros in from the right and let the leftmost bits fall off
```

- JavaScript Regular Expressions

```bash
Syntax /pattern/modifiers;
# In JavaScript, regular expressions are often used with the two string methods: search() and replace().
1. Modifiers > eg. [ i(case-insensitive matching), g(global match (find all)), m( multiline matching) # {i/g are also working as multiline so this maybe not needed}]

let text = "Visit W3Schools!";
let n = text.search("W3Schools"); # 6 # as it starts from 6th position
# i -> Means find case-insensitive words
let n = text.search(/W3SCHOol/i); # 6

let result = text.replace(/W3Schools/i, "Microsoft"); # It will replace w3 to microsoft
# g -> Global search, finds all instances of the search
let text = "Is this all there is?";
let result = text.match(/is/g); # [ 'is', 'is' ]
let result = text.match(/is/ig); # [ 'Is', 'is', 'is' ]

2. Patterns
    - Brackets are used to find a range of/individual characters # [abc], [a-z], (x|y)
    - Metacharacters are characters with a special meaning # \d \s \b \uxxxx
    - Quantifiers define quantities # n+, n*, n?

# --> Brackets []

# Find all the alphabets in the brackets [abc]
let result = text.match(/[is]/ig); # [ 'I', 's', 'i', 's', 'i', 's' ]

# Find all the alphabets from the range [0-9]
let result = text.match(/[a-h]/gi); # [ 'h', 'a', 'h', 'e', 'e' ]
let text = "123456789";
let result = text.match(/[1-4]/g); # [ '1', '2', '3', '4' ]

# Find any of the alternatives separated with | (x|y) --> Find 1st then seconod
let text = "re, green, red, green, gren, gr, blue, yellow";
let result = text.match(/(gr|green)/g); # [ 'gr', 'gr', 'gr', 'gr' ]
let result = text.match(/(green|gr)/g); # [ 'green', 'green', 'gr', 'gr' ]
let result = text.match(/(green|gr|red)/g); # [ 'green', 'red', 'green', 'gr', 'gr' ]

# --> Metacharacters /x

# \d -> Find a digit
let text = "Give 100%!";
let result = text.match(/\d/g); # [ '1', '0', '0' ]

# \s -> Find a whitespace character
let text = "Is this all there is?";
let result = text.match(/\s/g); # [ ' ', ' ', ' ', ' ' ]

# \b -> Matching the beginning or ending of the word {considers alphanumeric characters only?}
let text = "PLOa #LO2 HELLO(), Wow World?, LOOK AT YOU!";
let result = text.search(/LO\b/); # 13 # after HELLO ignoring parenthesis "()"
let result2 = text.search(/\bLO/); # 6 # before LO2 ignoring hastag "#"

# \uxxxx -> Find the Unicode character specified by the hexadecimal number xxxx
let result = text.match(/\u0057/g); # [ 'W', 'W' ]
let result = text.match(/\u0057/gi); # [ 'W', 'w', 'W' ]

# --> Quantifiers n_
let text = "Hellooo World! Helloo looool! ooooo lol";
# n+ ->  [same],[++infinite (ifSame-lastnumber)] --> Can't be less
let result = text.match(/ooo+/g); # [ 'ooo', 'oooo', 'ooooo' ]
let result = text.match(/loo+/g); # [ 'looo', 'loo', 'loooo' ]
let result = text.match(/(oo)+/g); # [ 'oo', 'oo', 'oooo', 'oooo' ] # oo as single character
# n* -> [same],[-1 (ifSame)],[++infinite (ifSame)]
let result = text.match(/ooo*/g); # [ 'ooo', 'oo', 'oooo', 'ooooo' ]
let result = text.match(/loo*/g); # [ 'looo', 'loo', 'loooo', 'lo' ]
let result = text.match(/(oo)*/g); # [ 'oo', 'oo', 'oooo', 'oooo', " "," ",.. ] + all spaces
# n? -> [same],[-1 (ifSame)] --> Can't be more
let result = text.match(/ooo?/g); # [ 'ooo', 'oo', 'ooo', 'ooo', 'oo' ]
let result = text.match(/loo?/g); # [ 'loo', 'loo', 'loo', 'lo' ]
let result = text.match(/(oo)?/g); # [ 'oo', 'oo', 'oo','oo', 'oo','oo', " ",.. ] + all spaces

 # .test() -> It searches a string for a pattern, and returns true or false
/est/.test("The best things in life are free!"); # true
# SAME AS ABOVE ONE LINE
const pattern = /e/;
const string = "The best things in life are free!"
pattern.test(string); # true

# .exec() -> it searches a string for a specified pattern, and returns an object.
/est/.exec("The best things in life are free!") # [...,index:5,...]
# If not found then returns null
/estasd/.exec("The best things in life are free!") # null
```

- JavaScript Errors
  - The try statement defines a code block to run (to try).
  - The catch statement defines a code block to handle any error.
  - The finally statement defines a code block to run regardless of the result.
  - The throw statement defines a custom error.

```bash

let message = "";
let x = "1";
try {
  if (x.trim() == "") throw "is empty";
  if (isNaN(x)) throw "is not a number";
  x = Number(x);
  if (x > 10) throw "is too high";
  if (x < 5) throw "is too low";
} catch (err) {
  message = "Error: " + err + ".";
  console.log(message);
} finally {
  console.log("Done");
}

# The Error Object - have two properties 1. name and 2. message
1.EvalError---   	  An error has occurred in the eval() function (NOW SyntaxError)
2.RangeError  	    A number "out of range" has occurred
3.ReferenceError 	  An illegal reference has occurred
4.SyntaxError 	    A syntax error has occurred
5.TypeError   	    A type error has occurred
6.URIError    	    An error in encodeURI() has occurred

# 2. RangeError
let num = 1;
try {
  num.toPrecision(500); # A number cannot have 500 significant digits eg 6 (92.6560)
} catch (err) {
  console.log(err.name); # RangeError
}

# 3. ReferenceError
let num = 1;
try {
  x = y + 1; # y cannot be used (referenced)
} catch (err) {
  console.log(err.name); # ReferenceError
}

# 4. SyntaxError
try {
  eval("alert('Hello)"); # Missing ' will produce an error
} catch (err) {
  console.log(err.name); # SyntaxError
}

# 5. TypeError
let x = 1;
try {
  num.toUpperCase(); # You cannot convert a number to upper case
} catch (err) {
  console.log(err.name); # ReferenceError # Should give TypeError
}

# 6. URIError
try {
  decodeURI("%%%");   # You cannot URI decode percent signs
} catch (err) {
  console.log(err.name); # URIError
}

```

- JavaScript Scope
  - Block scope
  - Function scope
  - Global scope
    - Variables created without a declaration keyword (var, let, or const) are always global, even if they are created inside a function.

```bash
1. Block Scope
# Variables declared inside a { } block cannot be accessed from outside the block -(let,const)
# Variables declared with the var keyword can NOT have block scope.
# EG IF-ELSE / LOOPS
{
  let x = 2;
  var y = 2;
}
// x can NOT be used here but // y CAN be used here

2. Function/Local Scope
# Variables declared within a JavaScript function, are LOCAL to the function
# Variables declared with var, let and const are quite similar when declared inside a function.

# HERE VAR IS NOT ACCESSIBLE OUTSIDE THE FUNCITON
myFunction(); # Function is called
console.log(carName); # ERROR
function myFunction() {
  var carName = "Volvo"; #CANNOT ACCESS OUTSITE JUST LIKE CONST AND LET
}
console.log(carName); # ERROR


3. Global Scope
# A variable declared outside a function, becomes GLOBAL.

4. Automatically Global
# If function scope variable is not declared and is """called after the function call""" then you can access the variable

# Example1:
// console.log(a); # Error
// console.log(b); # Error
// console.log(c); # Error
// console.log(d); # Error

check();
// console.log(a); # Error
// console.log(b); # Error
// console.log(c); # Error
console.log(d); // 4 # We can get the value of b after the function is called

function check() {
  let a = 1;
  const b = 2;
  var c = 3;
  d = 4;
}

5. Global Variables in HTML
# With JavaScript, the global scope is the JavaScript environment.
# In HTML, the global scope is the window object.
# Global variables defined with the var keyword belong to the window object:
Do NOT create global variables unless you intend to.

var carName1 = "Volvo";
let carName2 = "Volvo";
// code here can use window.carName1
// code here can not use window.carName2

# /////////////
for (let a = 0; a < 4; a++) {
  setTimeout(() => console.log(a), 2000);
} # 0,1,2,3

for (var a = 0; a < 4; a++) {
  setTimeout(() => console.log(a), 2000);
} # 4,4,4,4 # It's 4 and not 3 because a++ increase the value of a and then it compares

# ‘var’ is not block scoped but it is function scoped. So if we run the code below:
for (var a = 0; a < 4; a++) {
  (function (a) {
    setTimeout(() => console.log(a), 2000);
  })(a);  # 0,1,2,3 // passing a variable here
}

for (var a = 0; a < 4; a++) {
  (function () {
    var index = a; # can use let or const as inside function block all works similar
    setTimeout(() => console.log(index), 2000);
  })();  # 0,1,2,3 // without passing any variable here
}

# since ‘var’ variables are not block scoped, we did not create a new variable, instead we just re-assigned the existing variable and gave it new value

# If condition is passed, logic is executed inside the for block, in this case closure is created because setTimeout() is a function and it has another function inside it which is referencing outer variable ‘i’, so setTimeout is not actually executed directly, it is sent to WEB API and function inside it remembers reference to variable ‘i’ (not value — but reference)

FOR EXPLAINATION : https://medium.com/@jubomdivnishvili/the-mystery-behind-settimeout-in-loop-var-vs-let-behavior-in-depth-b56468d6a3d6

```

- JavaScript Hoisting
- Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).

  - In JavaScript, a variable can be declared after it has been used.
  - In other words; a variable can be used before it has been declared.
  - Hoisting applies to variable declarations(eg x=1) and to function declarations(eg function(){}) [and not Function Expressions (eg. const a = function() {})]- [Arrow function is also type of function expression ]
  - class declarations are not hoisted

- TLDR : Only the declaration of var(var x;)[can declare before it is used] is hoisted(moved to top), but initializing/assigning of value(x = 2;) needs to be applied before it is used (else x = undefined)::: (let will give referance error if not declared before and const gives syntex error as we can't reassigne a value)

- Variables defined with let and const are hoisted to the top of the block, but not initialized.
- Meaning: The block of code is aware of the variable, but it cannot be used until it has been declared.

- To avoid bugs, always declare all variables at the beginning of every scope.

- var:: Variable declaration will be hoisted, initialized as undefined
- let:: Hoisted but not initialized, will give error

```bash

# ----> var
x = 5;
var x; # This will work

# If var is initialize before or assigne before than it will work else give undefined (not error)
var a = 4; # Initialize a
console.log(a, b, c); # 4 undefined undefined
b = 5; # Assign 5 to b
console.log(a, b, c); # 4 5 undefined
var b; # Declare b
var c = 3; # Initialize c # only the declaration (var c), not the initialization (=3) is hoisted to the top. (So undefined)

# ----> let ,const

# Variables defined with let and const are hoisted to the top of the block, but not initialized.
# Meaning: The block of code is aware of the variable, but it cannot be used until it has been declared.


# let will give ReferenceError
x = 5; # ReferenceError: Cannot access 'a' before initialization
let x;

# const will give SyntaxError -> As value of const cannot be changed
x = 5;
const x; # SyntaxError (This code will not run)

```

- JavaScript Use Strict

- Normal variables in JavaScript can't be deleted using the delete operator.
- In strict mode, an attempt to delete a variable will throw an error and is not allowed. The delete operator can only delete properties on an object.

```bash
# Strict mode is declared by adding "use strict"; to the beginning of a script or a function.

x = 3.14;       # This will not cause an error.
myFunction();
"use strict"; # After this  undeclared variables will cause error
x = 3.14;       # This will cause an error because x is not declared
function myFunction() {
  y = 3.14;   # This will cause an error
}

#
# Using a variable, without declaring it, is not allowed
x = 3.14;                // This will cause an error
# Using an object, without declaring it, is not allowed
x = {p1:10, p2:20};      // This will cause an error
# Deleting a variable (or object) is not allowed
let x = 3.14;
delete x;                // This will cause an error
# Deleting a function is not allowed.
function x(p1, p2) {};
delete x;                // This will cause an error
# Duplicating a parameter name is not allowed
function x(p1, p1) {};   // This will cause an error
# If the object is not specified, functions in strict mode will return undefined and functions in normal mode will return the global object (window):
function myFunction() {
  alert(this); // will alert "undefined"
}
myFunction();
# +++++++++++++
```

- The JavaScript this Keyword
  - this is not a variable. It is a keyword. You cannot change "this" to some other value/keyword.

```bash
# this in a Method => When used in an object method, this refers to the object.(person object)
const person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  fullName : function() {
    return this.firstName + " " + this.lastName; # This is the person object
  }
};

# "this" Alone ==> When used alone, this refers to the global object. ( same in strict object)
let x = this; # In a browser window the global object is [object Window]

# "this" in a Function => In a function, the global object is the default binding for this.
function myFunction() {
  return this; # In a browser window the global object is [object Window]:
}

# "this" in a Function (Strict) => JavaScript strict mode does not allow default binding.
"use strict";
function myFunction() {
  return this; # So, when used in a function, in strict mode, this is undefined.
}

# "this" in Event Handlers => In HTML event handlers, this refers to the HTML element that received the event
<button onclick="this.style.display='none'">
  Click to Remove Me! # Will apply to button
</button>

# ====> Explicit Function Binding
# The call() and apply() methods are predefined JavaScript methods.
# They can both be used to call an object method with "another object" as argument.

const person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
const person2 = {
  firstName:"John",
  lastName: "Doe",
}
# this refers to person2, even if fullName is a method of person1
person1.fullName.call(person2); # Return "John Doe":

# ==> Function Borrowing {Full explaination in upcoming section}
# With the bind() method, an object can borrow a method from another object.
const person = {
  firstName:"John",
  lastName: "Doe",
  fullName: function () {
    return this.firstName + " " + this.lastName;
  }
}
const member = {
  firstName:"Hege",
  lastName: "Nilsen",
}
# The member object borrows the fullname method from the person object
let fullName = person.fullName.bind(member);

```

- JavaScript Arrow Function (lambda expressions)

  - Normal Function:

    - Suitable for methods within objects where "this" needs to refer to the object.
    - Useful when "arguments" object is needed.
    - Can be used as constructors.
    - Can call a function above it is defined

  - Arrow Function:

    - Ideal for callbacks or functions that do not require their own "this" context.
    - More concise syntax, especially for inline functions.
    - Cannot be used as constructors.
    - Can't call a function above it is defined

```bash
hello = () => {
  return "Hello World!";
}
# Arrow Functions Return Value by Default:
hello = () => "Hello World!";

1. this Binding

# ==> normal function:
# The value of this is dynamic and depends on how the function is called.
# Can be used as methods in objects where this refers to the object.
const obj = {
  value: 10,
  method: function () {
    return this.value;
  },
};
console.log(obj.method()); // 10

# ==> arrow function:
# The value of this is lexically bound, meaning it takes this from its surrounding context at the time the function is defined, not at the time it is called.
# Arrow functions are not suitable for methods that require their own this.
const obj = {
  value: 10,
  method: () => {
    return this.value; // "this" here is not "obj", but the enclosing scope when the arrow function was defined.
  },
};
console.log(obj.method()); // undefined (or the value of "this" in the enclosing scope)

2. arguments Object

# ==> normal function:
# Has access to the arguments object which contains all arguments passed to the function.
function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}
console.log(sum(1, 2, 3)); // 6

# ==> arrow function:
const sum = (...args) => {
    return args.reduce((total, current) => total + current, 0);
};
console.log(sum(1, 2, 3)); // 6

3. Constructor

# ==> normal function:
# Can be used as constructors and called with the new keyword to create instances.
function Person(name) {
    this.name = name;
}
const person = new Person('John');
console.log(person.name); // John

# ==> arrow function:
# Cannot be used as constructors. Attempting to use new with an arrow function will result in an error.
const Person = (name) => {
    this.name = name;
};
const person = new Person('John'); # Error: Person is not a constructor
```

- JavaScript Classes

- The Constructor Method
  - It has to have the exact name "constructor"
  - It is executed automatically when a new object is created
  - It is used to initialize object properties
- Class Methods
  - function of that class (for object)

```bash
# A JavaScript class is not an object. It is a template for JavaScript objects.

# If you do not define a constructor method, JavaScript will add an empty constructor method

# creates a class named "Car". it has two initial properties: "name" and "year".
# Created a Class method named "age", that returns the Car age
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }
  age() {
    const date = new Date();
    return date.getFullYear() - this.year;
  }
  ageAdd(x) { # You can send parameters to Class methods
    return this.age() + x;
  }
}
const myCar = new Car("Ford", 1998); # uses the Car class to create two Car objects
console.log(myCar.age()); # 26
console.log(myCar.ageAdd(5)); # 31

```

- JavaScript Modules
  - Modules only work with the HTTP(s) protocol.
  - A web-page opened via the file:// protocol cannot use import / export.

```bash
1. Export

# ==> Named Exports

# In-line individually:
export const name = "Jesse";
export const age = 40;

# All at once at the bottom:
const name = "Jesse";
const age = 40;
export {name, age}; # Import like this :: import { name, age } from "./person.js";

# ==> Default Exports
const message = () => {
const name = "Jesse";
const age = 40;
return name + ' is ' + age + 'years old.';
};
export default message; # Import like this :: import message from "./message.js";

2. Import

# Import from named exports
import { name, age } from "./person.js";

# Import from default exports

import message from "./message.js";

```

- JavaScript JSON
  - JSON (JavaScript Object Notation) is a format for storing and transporting data.
  - JSON is language independent
    - [The JSON syntax is derived from JavaScript object notation syntax, but the JSON format is text only. Code for reading and generating JSON data can be written in any programming language.]

```bash
# ==> JSON Syntax Rules
# Data is in name/value pairs
# Data is separated by commas
# Curly braces hold objects
# Square brackets hold arrays

let text = "employees":[
  {"firstName":"John", "lastName":"Doe"},
  {"firstName":"Anna", "lastName":"Smith"},
  {"firstName":"Peter", "lastName":"Jones"}
]

# Converting a JSON Text to a JSON -> To use in JS File
const obj = JSON.parse(text);
# When receiving the data from a web server, the data is always in a string format. But you can convert this string value to a javascript object using parse() method.

# Converting a JSON to a JSON Text --> To transfer over
const obj = JSON.stringify(text);
# When sending data to a web server, the data has to be in a string format. You can achieve this by converting JSON object into a string using stringify() method.
```

- JavaScript Debugging

```bash
# The debugger Keyword is same as Setting Breakpoints (if debugger turned on)

let x = 15 * 5;
debugger; # If the console is opened in browser then the code will stop here
console.log(x);

```

- JavaScript Style Guide

```bash
# Always end a simple statement with a semicolon.
const cars = ["Volvo", "Saab", "Fiat"]; # semicolon
const person = {
  firstName: "John",
  lastName: "Doe",
 };  # semicolon

# Do not end a complex statement with a semicolon.
function toCelsius(fahrenheit) {
  return (5 / 9) * (fahrenheit - 32);
} # no semicolon
for (let i = 0; i < 5; i++) {
  x += i;
} # no semicolon
if (time < 20) {
  greeting = "Good day";
} else {
  greeting = "Good evening";
} # no semicolon

# PascalCase: => first character of every word is Capital (MyNameIs)
# camelCase: => first character of every word is Capital except first word (myNameIs)

```

- JavaScript Best Practices

```bash
# Avoid global variables, avoid new, avoid ==, avoid eval()
# Always Declare Local Variables
# Declarations on Top
# Initialize Variables :=> It is a good coding practice to initialize variables when you declare them.
# Declare Objects and Arrays with const

# ==> Don't Use new Object()
# Use "" instead of new String()
# Use 0 instead of new Number()
# Use false instead of new Boolean()
# Use {} instead of new Object()
# Use [] instead of new Array()
# Use /()/ instead of new RegExp()
# Use function (){} instead of new Function()

let x1 = "";             // new primitive string
let x2 = 0;              // new primitive number
let x3 = false;          // new primitive boolean
const x4 = {};           // new object
const x5 = [];           // new array object
const x6 = /()/;         // new regexp object
const x7 = function(){}; // new function object

# Beware of Automatic Type Conversions
let x = 5 + 7;                                # x.valueOf() is 12,  typeof x is a number
let x = 5 + "7";                              # x.valueOf() is 57,  typeof x is a string
let x = "5" + 7;                              # x.valueOf() is 57,  typeof x is a string
let x = 5 - 7;                                # x.valueOf() is -2,  typeof x is a number
let x = 5 - "7";                              # x.valueOf() is -2,  typeof x is a number
let x = "5" - 7;                              # x.valueOf() is -2,  typeof x is a number
let x = 5 - "x";                              # x.valueOf() is NaN, typeof x is a number

let x = "Hello" - "Dolly";    // returns NaN and not an error

# Use === Comparison
0 == "";                                                # true
1 == "1";                                               # true
1 == true;                                              # true

0 === "";                                               # false
1 === "1";                                              # false
1 === true;                                             # false

# Use Parameter Defaults
function (a=1, b=1) { /*function code*/ } # If value is not passed


# End Your Switche block with Defaults

# ==> Avoid creating Number, String, and Boolean as Objects
# Declaring these types as objects, slows down execution speed, and produces nasty side effects:
let x = "John";
let y = new String("John");
(x === y) // is false because x is a string and y is an object.

let x = new String("John");
let y = new String("John");
(x == y) // is false because you cannot compare objects.
```

- JavaScript Common Mistakes

```bash
# Accidentally Using the Assignment Operator
let x = 0;
if (x == 10) # false as expected
if (x = 10) # true as 10 value is true (always)
if (x = 0) # false as 0 value is false (always)

# switch statements use strict comparison:
let x = 10;
switch(x) {
  case 10: alert("Hello"); # This will alert
}
switch(x) {
  case "10": alert("Hello"); # This won't alert
}

# ==> Confusing Addition & Concatenation. As both uses + operator
# Addition is about adding numbers.
# Concatenation is about adding strings.
let x = 10;
x += 5; # 15
x += "5"; # 105 # 155

# Misunderstanding Floats
# All programming languages, including JavaScript, have difficulties with precise floating point values:
let x = 0.1;
let y = 0.2;
let z = x + y; # 0.30000000000000004 # the result in z will not be 0.3
let z = (x * 10 + y * 10) / 10; # 0.3       // z will be 0.3

# Breaking a JavaScript String (using \)
let x = "Hello \
World!"; # Hello World!

# Misplacing Semicolon
if (x == 19);
{
  // code block will run everytime
}

# Breaking a Return Statement ==> Never break a return statement.
# If a statement is incomplete JS will try to complete the statement by reading the next line: [eg let]
# But since this statement is complete, JS will automatically close it like this: [eg return]
function myFunction(a) {
  let
  power = 10; # let power = 10; make this
  return # return undefined
  a * power; # This won't be executed
}

# In JavaScript, arrays use numbered indexes: (NOT named indexes.)
const person = [];
person[0] = "John"; # Will add
person["firstName"] = "John"; # Won't add

# JSON does not allow trailing commas.
points = [40, 100, 1, 5,]; # Errror in JSON
points = [40, 100, 1, 5]; # No error

# Undefined is Not Null
let x = null;
let y = undefined;
console.log(typeof x);                                  # object
console.log(typeof y);                                  # undefined
console.log(typeof y === "undefined");                  # true
console.log(x === undefined);                           # false
console.log(x === "undefined");                         # false
console.log(x === null);                                # true -> IT'S TRUE AND NOT FALSE
console.log(x === "null");                              # false

```

- JavaScript Performance

```bash
# ==> Reduce Activity in Loops
for (let i = 0; i < arr.length; i++) { # arr.length will run on every iteration

let l = arr.length; # arr.length will run once
for (let i = 0; i < l; i++) {

# ==> Reduce DOM Access, also Reduce DOM Size
# Accessing the HTML DOM is very slow, compared to other JavaScript statements.
# If you expect to access a DOM element several times, access it once, and use it as a local variable:
const obj = document.getElementById("demo");
obj.innerHTML = "Hello";

# ==>Avoid Unnecessary Variables:  if you don't plan to save values later
let fullName = firstName + " " + lastName;
console.log(fullName);

console.log(firstName + " " + lastName);

# ==> Avoid Using "with": It has a negative effect on speed.
# "with" keyword is not allowed in strict mode.
```

- JavaScript Object Definition

- Methods for Defining JavaScript Objects
  - Using an Object Literal
  - Using the new Keyword
  - Using an Object Constructor
  - Using Object.assign()
  - Using Object.create()
  - Using Object.fromEntries()

```bash
1. Using an Object Literal
2. Using the new Keyword

# Create an Object
const person = {}; # object literal is also callled an object initializer.
const person = new Object(); # Use above instead of this

# Add Properties
person.firstName = "John";
person.lastName = "Doe";

3. Using an Object Constructor
#  to create many objects of the same type.

# Create Object Type Person
function Person(first, last, age) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = blue;
}
# we can use new Person() to create many new Person objects:
const myFather = new Person("John", "Doe", 50);
const myMother = new Person("Sally", "Rally", 48);

```

- JavaScript Object Prototypes

```bash
# ==> Prototype Inheritance
# -> All JavaScript objects inherit properties and methods from a prototype:
# Date objects inherit from Date.prototype
# Array objects inherit from Array.prototype
# Person objects inherit from Person.prototype

# Adding Properties and Methods to Objects :: Using the prototype Property
# to add new properties (or methods) to all existing objects of a given type. or to an object constructor. BUT Only modify your own prototypes. Never modify the prototypes of standard JavaScript objects.

function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.nationality = "English";
Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};

```

- JavaScript Object Methods
  - General Methods
  - Property Management Methods
  - Object Protection Methods

1. General Methods

```bash
# Copies properties from a source object to a target object
Object.assign(target, source)

# Creates an object from an existing object
Object.create(object)

# Returns an array of the key/value pairs of an object
Object.entries(object)

# Creates an object from a list of keys/values
Object.fromEntries()

# Returns an array of the keys of an object
Object.keys(object)

# Returns an array of the property values of an object
Object.values(object)

# Groups object elements according to a function
Object.groupBy(object, callback)

1. ==> Object.assign(target, source) # Copies properties from a source object to a target object

# Create Target Object
const person1 = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};
# Create Source Object
const person2 = {firstName: "Anne",lastName: "Smith"};
# Assign Source to Target
Object.assign(person1, person2); # { firstName: 'Anne', lastName: 'Smith', age: 50, eyeColor: 'blue' } #-> firstName and lastName is replaced in person1

# USE OBJECT.ASSIGN TO CREATE A COPY OF OBJECT BY VALUE INSTEAD OF REFERANCE
#@@@ But be aware this is a shallow copy - nested objects are still copied as reference.
# FOR NESTED/DEEP OBJECTS USE: structuredClone() OR JSON.parse(JSON.stringify(x)) ???
const x = { a: "me", b: "you" };
const y = x; # IT IS COPIED BY REFERANCE
const z = Object.assign( {}, x); # IT IS COPIED BY VALUE
console.log(x, y, z); # { a: 'me', b: 'you' } { a: 'me', b: 'you' } { a: 'me', b: 'you' }
delete x.a;
console.log(x, y, z); # { b: 'you' } { b: 'you' } { a: 'me', b: 'you' }


2. ==> Object.create(object)   # Creates an object from an existing object

function fruits() {
  this.name = "franco";
}
function fun() {
  fruits.call(this);
}

fun.prototype = Object.create(fruits.prototype);
const app = new fun();
console.log(app.name);

3. ==> Object.entries(object)  # Returns an array of the key/value pairs of an object

let text = Object.entries(person1); # [ [ 'firstName', 'John' ],..[ 'eyeColor', 'blue' ] ]

# Object.entries() makes it simple to use objects in loops:
for (let [a, b] of text) {
  console.log( a, b); # firstName John, lastName Doe, age 50, eyeColor blue
}


4. ==> Object.fromEntries()    # Creates an object from a list of keys/values

const fruits = [
  ["apples", 300],
  ["pears", 900],
  ["bananas", 500],
];
const myObj = Object.fromEntries(fruits); # { apples: 300, pears: 900, bananas: 500 }


5. ==> Object.keys(object) # Returns an array of the keys of an object

const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue",
};
let text = Object.keys(person); # [ 'firstName', 'lastName', 'age', 'eyeColor' ]

6. ==> Object.values(object)   # Returns an array of the property values of an object

const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue",
};
let text = Object.values(person); # [ 'John', 'Doe', 50, 'blue' ]


7. ==> Object.groupBy(object, callback)    # Groups object elements according to a function

# It's new so don't use it #########
// Create an Array
const fruits = [
  { name: "apples", quantity: 300 },
  { name: "bananas", quantity: 500 },
  { name: "oranges", quantity: 200 },
  { name: "kiwi", quantity: 150 },
];

// Callback function to Group Elements
function myCallback({ quantity }) {
  return quantity > 200 ? "ok" : "low";
}

// Group by Quantity
const result = Object.groupBy(fruits, myCallback);

8. JavaScript for...in Loop # to loops through the properties of an object.

const person = {
  fname: "John",
  lname: "Doe",
  age: 25,
};

for (let x in person) {
  console.log(person[x]); # John, Doe, 25
}

```

2. Property Management Methods -----------

```bash

```

3. Object Protection Methods

```bash

1. => const # Prevents re-assignment

const car = {type:"Fiat", model:"500", color:"white"}; # cannot reassign value to car (car =)


2. => Object.preventExtensions(object) # Prevents adding object properties
# TO STOP ADDING ANY NEW PROPERTY TO OBJECT / ARRAY (as array are also objects)

# OBJECT
const person = {firstName:"John", lastName:"Doe"};
Object.preventExtensions(person); # Prevent Adding new properties to person object
person.nationality = "English"; # This will throw an error

# ARRAY
const fruits = ["Banana", "Orange", "Apple", "Mango"];
Object.preventExtensions(fruits); # Prevent Adding new elements to fruits array
fruits.push("Kiwi"); # This will throw an error

3. => Object.isExtensible(object) # Returns true if properties can be added to an object

let answer = Object.isExtensible(person); # This will return false (AS PREVENTED ABOVE)
let answer = Object.isExtensible(fruits); # This will return false (AS PREVENTED ABOVE)


4. => Object.seal(object) # Prevents adding and deleting object properties

# OBJECT
const person = {firstName:"John", lastName:"Doe"};
Object.seal(person); # Prevent Adding+Removing new properties to person object
delete person.lastName; # This will throw an error

# ARRAY
const fruits = ["Banana", "Orange", "Apple", "Mango"];
Object.seal(fruits); # Prevent Adding+Removing new elements to fruits array
fruits.pop("Kiwi"); # This will throw an error


5. => Object.isSealed(object) # Returns true if object is sealed

let answer = Object.isSealed(person); # This will return false (AS PREVENTED ABOVE)
let answer = Object.isSealed(fruits); # This will return false (AS PREVENTED ABOVE)


6. => Object.freeze(object) # Prevents any changes to an object

# OBJECT
const person = {firstName:"John", lastName:"Doe"};
Object.freeze(person); # Prevent any changes to person object
person.lastName = "Nodoe"; # This will throw an error

# ARRAY
const fruits = ["Banana", "Orange", "Apple", "Mango"];
Object.freeze(fruits); # Prevent any changes to fruits array
fruits.pop("Kiwi"); # This will throw an error

# Remember freezing is only applied to the top-level properties in objects but not for nested objects.
const user = {
  name: "John",
  employment: {
    department: "IT",
  },
};
Object.freeze(user);
user.employment.department = "HR"; # WORKS FINE

7. => Object.isFrozen(object) # Returns true if object is frozen

let answer = Object.isFrozen(person); # This will return false (AS PREVENTED ABOVE)
let answer = Object.isFrozen(fruits); # This will return false (AS PREVENTED ABOVE)


```

- JavaScript Object Accessors (Getters and Setters)

```bash
# JavaScript Getter (The get Keyword)
# JavaScript Setter (The set Keyword)
# ==> Why Using Getters and Setters?
# It gives simpler syntax
# It allows equal syntax for properties and methods (without using "()" in methods)
# It can secure better data quality
# It is useful for doing things behind-the-scenes

# THIS IS DIFFERENT FROM FUNCTION OBJECT CREATION: THIS WILL ONLY WORK FOR THIS OBJECT
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "en",
  lang1: function () {
    return this.language;
  }, # call by person.lang1()
  lang2: function (value) {
    return (this.language = value);
  },, # call by person.lang1("OK")
  get lang3() {
    return this.language;
  },, # call by person.lang1 --> parenthesis is not needed
  set lang4(value) {
    return (this.language = value);
  },, # call by person.lang1 = "OK" --> assign value and not inside parenthesis
};

console.log( person.lang1()); # en
console.log( person.lang3); # en
person.lang2( "Hindi");
console.log( person.lang1()); # Hindi
console.log( person.lang3); # Hindi
person.lang4 = "Gujarati";
console.log( person.lang1()); # Gujarati
console.log( person.lang3); # Gujarati

```

- JavaScript Function Definitions

- A function defined as the property of an object, is called a method to the object.
- A function designed to create new objects, is called an object constructor.

```bash
1. ==> Function Declarations
function myFunction(a, b) {
  return a * b;
}

2. ==> Function Expressions
# The function below ends with a semicolon because it is a part of an executable statement.
const x = function (a, b) {
  return a * b;
};

3. ==> The Function() Constructor
# You actually don't have to use the function constructor. The example above is the same as writing:
const myFunction = new Function("a", "b", "return a * b");

4. ==> Function Hoisting
# Hoisting applies to variable declarations and to function declarations. So, JS functions can be called before they are declared:
myFunction(5); # This won't give error
function myFunction(y) {
  return y * y;
}

# Functions defined using an expression are not hoisted.
myFunction(5); # This will give error
const myFunction = function (y) {
  return y * y;
};
# Arrow function is also type of function expression so it will also give error
myFunction(5); # This will give error
const myFunction = (y) => {
  return y * y;
};

5. ==> Self-Invoking Functions - IIFE(immediately-invoked function expression)
# It is used to keep the namespace clean, increase the code readability, and introduce private data and methods.

# Function Declarations -> (function without name)
(function () {
  let x = "Hello!!";
  console.log(x); # This will be loged by itself
})();
# Function Expressions
const x = (function () {
  let x = "Hello!!";
  console.log(x); # This will be loged by itself
})();
# Arrow function
const y = (() => {
  let x = "Hello!!";
  console.log(x); # This will be loged by itself
})();

# passing arguments
const y = "OK";

(function (my_Y) { # here is the parameters
  let x = "Hello!!";
  console.log(x + my_Y);
})(y); # here pass arguments

6. ==> Functions Can Be Used as Values

function myFunction(a, b) {
  return a * b;
}
let x = myFunction(4, 3) * 2;

7. ==> Functions are Objects
# The typeof operator in JavaScript returns "function" for functions. But, it can best be described as objects.
# JavaScript functions have both properties and methods.

# arguments.length property
function myFunction(a, b) {
  console.log(arguments[0]); # 1
  return arguments.length;
}
myFunction(1, 2);

# toString() method
function myFunction(a, b) {
  return a * b;
}
let text = myFunction.toString(); # give whole function as string


8. ==> Arrow Functions
# Arrow functions allows a short syntax for writing function expressions.
# Arrow functions do not have their own this. They are not well suited for defining object methods.(funciton(name){this.name=name})
# Arrow functions are not hoisted. They must be defined before they are used.
# Duplicate parameter name not allowed in arrow function in any mode, strict or non-strict
# ( allowed in function expression and function declaration in non-strict mode)
# Arrow functions do not have an arguments, super, this, or new.target bindings.

const x = (x, y) => { return x * y };
console.log(x(2, 5));

# You can only omit the return keyword and the curly brackets if the function is a single statement.
const x = (x, y) => x * y;
console.log(x(2, 5));

9. first order function
# A first-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value.
const firstOrder = () => console.log("I am a first order function!");

10. higher order function
# A higher-order function is a function that accepts another function as an argument or returns a function as a return value or both.
const firstOrderFunc = () =>
  console.log("Hello, I am a First order function");
const higherOrder = (ReturnFirstOrderFunc) => ReturnFirstOrderFunc();
higherOrder(firstOrderFunc);

11. unary function
# function that accepts exactly one argument.

12. currying function
# Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument.
# EXAMPLE1
function newFunc1(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}
console.log(newFunc1(1)(2)(3));

# EXAMPLE2
const newFunc2 = (a) => (b) => (c) => a + b + c;
console.log(newFunc2(4)(5)(6));

# EXAMPLE3
const evaluate = (operation) => (b) => (c) => {
  if (operation === "sum") return b + c;
  else if (operation === "substract") return b - c;
  else if (operation === "multiply") return b * c;
  else if (operation === "divide") return b / c;
  else return "Invalide Operation";
};
console.log(evaluate("sum")(6)(2)); # 8
console.log(evaluate("substract")(6)(2)); # 4
console.log(evaluate("multiply")(6)(2)); # 12
console.log(evaluate("divide")(6)(2)); # 3
console.log(evaluate("abc")(6)(2)); # "Invalide Operation"
# NOW JUST ADD EVERYTIME NO NEED TO CALL EVALUTE FUNCTION WITH SUM EVERYTIME
const add = evaluate("sum");
console.log(add(2)(5)); # 6
console.log(add(3)(6)); # 9

# EXAMPLE4 - INFINITE CURRYING
const addInfinitely = (a) => (b) => {
  if (b) return addInfinitely(a + b); # If any value is passed then return the addInfinitely function and start again
  return a; # If no value is passed then return the a (ie. the total value till now)
};
console.log( addInfinitely(2)(3)(5)()); # 10
console.log( addInfinitely(1)(2)(3)(4)(5)(6)(7)(8)(9)()); # 45



# WHY WE USE CURRING
  - To avoid passing same variable again and again
  - To create higher order functions
  - To make the function pure and less porne to errors

```

- JavaScript Function Parameters

  - Function "parameters" are the names listed in the function definition.
  - Function "arguments" are the real values passed to (and received by) the function.

  - Parameter Rules
    - JavaScript function definitions do not specify data types for parameters.
    - JavaScript functions do not perform type checking on the passed arguments.
    - JavaScript functions do not check the number of arguments received.

```bash
# Default Parameter Values
function myFunction(x = 0, y = 0) {
  return x + y;
}
myFunction(5); # Only x is provided

# Function Rest Parameter
# The rest parameter (...) allows a function to treat an infinite number of arguments as an array:
function sum(...args1) {
  console.log(args1); # [4, 9, 16, 25, 29, 100, 66, 77]
  let sum = 0;
  for (let arg of args1) sum += arg;
  return sum;
}
let x = sum(4, 9, 16, 25, 29, 100, 66, 77);

# The Arguments Object
# JavaScript functions have a built-in object called the arguments object. It contains an array of the arguments used when the function was called (invoked).

function myFunction() {
  console.log(arguments[0]); # 1
  return arguments.length;
}
myFunction(1, 2);

# Arguments are Passed by Value =>> If a function changes an argument's value, it does not change the parameter's original value.
# Objects are Passed by Reference =>> If a function changes an object property, it changes the original value.

```

- JavaScript Function Invocation

- If a function is not a method of a JavaScript object, it is a function of the global object

```bash
# The function below does not belong to any object. But in JavaScript there is always a default global object.
# In HTML the default global object is the HTML page itself, so the function below "belongs" to the HTML page.
# In a browser the page object is the browser window. The function below automatically becomes a window function.

function myFunction(a, b) {
  return a * b;
}
myFunction(10, 2);

# What is "this"?
  # - In an object method, this refers to the object.
  # - Alone, this refers to the global object.
  # - In a function, this refers to the global object. - OKKKKKK
  # - In a function, in strict mode, this is undefined. - OKKKKKK
  # - In an event, this refers to the element that received the event.
  # - Methods like call(), apply(), and bind() can refer this to any object.

let x = myFunction(); # x is window object in browser and in node it's "global" object

function myFunction() {
  return this;
}

# Invoking a Function as a Method
# The fullName method is a function. The function belongs to the object. myObject is the owner of the function.
const myObject = {
  firstName:"John",
  lastName: "Doe",
  fullName: function () {
    return this.firstName + " " + this.lastName;
  }
}
myObject.fullName(); # Will return "John Doe"

# Invoking a Function with a Function Constructor
# It looks like you create a new function, but since JavaScript functions are objects you actually create a new object -> "new" will create a object in function constructor and not a function itself

# This is a function constructor
function myFunction(arg1, arg2) {
  this.firstName = arg1;
  this.lastName  = arg2;
}
const myObj = new myFunction("John", "Doe"); # This creates a new object

myObj.firstName; # This will return "John"

```

- JavaScript Function call()

- With call(), an object can use a method belonging to another object.

```bash
# With call(), an object can use a method belonging to another object.
# eg. person1 object uses a fullName method belonging to person object
const person = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
const person1 = {
  firstName:"John",
  lastName: "Doe"
}
const person2 = {
  firstName:"Mary",
  lastName: "Doe"
}
person.fullName.call(person1); # This will return "John Doe":

# The call() Method with Arguments

const person = {
  fullName: function (city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  },
};

const person1 = {
  firstName: "John",
  lastName: "Doe",
};

person.fullName.call( person1, "Oslo", "Norway"); # John Doe,Oslo,Norway
```

- JavaScript Function apply()

  - The call() method takes arguments separately.
  - The apply() method takes arguments as an array.

```bash
const person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}

const person1 = {
  firstName:"John",
  lastName: "Doe"
}

person.fullName.apply(person1, ["Oslo", "Norway"]);

# Simulate a Max Method on Arrays
Math.max(1,2,3);                # Will return 3
Math.max.apply(null, [1,2,3]);  # Will also return 3
Math.max.apply(Math, [1,2,3]);  # Will also return 3 # As first argument is object
Math.max.apply(" ", [1,2,3]);   # Will also return 3
Math.max.apply(0, [1,2,3]);     # Will also return 3 # 0 won't effect the result as it's an object and not value itself

```

- JavaScript Function bind()

```bash

# Example1
const person = {
  name: "Alice",
  greet: function (greeting) {
    console.log(greeting + ", " + this.name);
  },
};
person.greet("Hello"); # "Hello, Alice"

const greet2 = person.greet; # Here the function greet was transfered but not 'this'
greet2("Hello"); # undefined, because `this` is not bound to `person`

const greet2 = person.greet.bind(person);
greet2("Hello"); # "Hello, Alice"

# When a function is used as a callback, "this" is lost.

# Example2
# the bind() method is used to bind person.display to person.
const person = {
  firstName: "John",
  lastName: "Doe",
  display: function () {
    console.log(this.firstName + " " + this.lastName);
  },
};

setTimeout(person.display, 1000); # undefined undefined
let display = person.display.bind(person);
setTimeout(display, 1000); # John Doe

```

- JavaScript Closures
- A closure is a function having access to the parent scope, even after the parent function has closed.
  - the function defined in the closure ‘remembers’ the environment in which it was created.
  - closure contains any and all local variables that were declared inside the outer enclosing function.

```bash

# EXECUTION CONTEXT
Execution context is an abstract concept used by the ECMAScript specification to track the runtime evaluation of code. This can be the global context in which your code is first executed or when the flow of execution enters a function body.

There are times when the running execution context is suspended and a different execution context becomes the running execution context. The suspended execution context might then at a later point pick back up where it left off.

# GLOBAL EXECUTOIN CONTEXT > EXECUTION CONTEXT (FOO) > EXECUTION CONTEXT (BAR)
# 1. GLOBAL EC - EVERTHING INSIDE A FILE
# 2. EC (FOO) - EVERTHING INSIDE FOO() FUNCTION
# 3. EC (BAR) - EVERTHING INSIDE BAR() FUNCTION

var x = 10;
function foo() {
  var y = 20; // free variable
  function bar() {
    var z = 15; // free variable
    return x + y + z;
  }
  return bar;
}

# LEXICAL ENVIRONMENT
every execution context has a Lexical Environment. This Lexical environments holds variables and their associated values, and also has a reference to its outer environment.

# TL;DR
Execution context is an abstract concept used by the ECMAScript specification to track the runtime evaluation of code. At any point in time, there can only be one execution context that is executing code.
Every execution context has a Lexical Environment. This Lexical environments holds identifier bindings (i.e. variables and their associated values), and also has a reference to its outer environment.
The set of identifiers that each environment has access to is called “scope.” We can nest these scopes into a hierarchical chain of environments, known as the “scope chain”.
Every function has an execution context, which comprises of a Lexical Environment that gives meaning to the variables within that function and a reference to its parent’s environment. And so it appears as if the function “remembers” this environment (or scope) because the function literally has a reference to this environment. This is a closure.
A closure is created every time an enclosing outer function is called. In other words, the inner function does not need to return for a closure to be created.
The scope of a closure in JavaScript is lexical, meaning it’s defined statically by its location within the source code.
Closures have many practical use cases. One important use case is to maintain a private reference to a variable in the outer scope.


```

```bash
# JavaScript Nested Functions
# JavaScript supports nested functions. Nested functions have access to the scope "above" them.

const plus = (() => {
  let counter = 0;
  console.log("Runs once"); # It only runs once
  return () => ++counter;
})();
console.log(plus());
console.log(plus());
console.log(plus());

# Example Explaination
    # The variable "plus" is assigned to the return value of a self-invoking function.
    # The self-invoking function only runs once. It sets the counter to zero (0), and returns a function expression.
    # This way "plus" becomes a function. The wonderful part is that it can access the counter in the parent scope.
    # This is called a JavaScript "closure". It makes it possible for a function to have "private" variables.
    # The counter is protected by the scope of the anonymous function, and can only be changed using the add function.

# Question and Answer
# when function calling itself then first it increase to 1 then plus() is called so it should become 2 but it start from 1 why ??????????
# BECAUSE IT IS RETURNING THE FUNCITON EXPRESSION AND NOT CALLING THE FUNCITON. FUNCITON IS ONLY CALLED BY THE PLUS VARIABLE

# ADD MORE CLOSURE EXAMPLES

# EXAMPLE 1
function makeAdder(x) {
  return (y) => x + y;
}

const add5 = makeAdder(5);
const add10 = makeAdder(10);

console.log(add5(2)); // 7
console.log(add10(2)); // 12

# EXAMPLE 2
function find() {
  const a = [];
  for (let i = 0; i < 10000000; i++) {
    a[i] = i * i;
  }
  return (index) => {
    console.log(a[index]);
  };
}
const newFind = find(); # IT WILL FIRST RUN THE LOOP
console.time("10");
newFind(10); # NOW WILL JUST FIND THE VALUE AND NOT RUN THE LOOP EVERYTIME
console.timeEnd("10");

console.time("100");
newFind(100);
console.timeEnd("100");

# EXAMPLE 2
function check() {
  for (var i = 0; i < 3; i++) {
    ((i) => {
      setTimeout(() => console.log(i), i * 1000);
    })(i);
  }
}
check();

# EXAMPLE 3
function counter() {
  let _counter = 0;
  function add(value = 1) {
    _counter += value;
  }
  function substract(value = 1) {
    _counter -= value;
  }
  function display() {
    console.log("Total counter is " + _counter);
    return "Total counter is " + _counter;
  }
  return { add, substract, display };
}

const myCounter = counter();
myCounter.display(); // 0
myCounter.add(3);
myCounter.add(2);
myCounter.display(); // 5
myCounter.substract(2);
myCounter.display(); // 3

const myCounter2 = counter();
myCounter2.display(); // 0
myCounter2.add();
myCounter2.add();
myCounter2.add();
myCounter2.display(); // 3


```

- JavaScript Classes <- (Search this for class intro info about classes around 2152 line )

```bash
1. ==>  Class Inheritance

# To create a class inheritance, use the extends keyword.
# A class created with a class inheritance inherits all the ""methods"" from another class:
class Car {
  constructor(brand) {
    this.carname = brand;
  }
  present() { # this method will automatically inherited
    return 'I have a ' + this.carname;
  }
}
# car class is inherited to model class
class Model extends Car {
  constructor(brand, mod) {
    super(brand); #  accessing to the parent's properties and methods.
    this.model = mod;
  }
  show() {
    return this.present() + ', it is a ' + this.model;
  }
}
let myCar = new Model("Ford", "Mustang");

# use the get and set, if you want to do something special with the value before returning them, or before you set them.
# The name of the getter/setter method cannot be the same as the name of the property, in this case carname, use _ to separate property name from get/set
# You can use same name for get and set
class Car {
  constructor(brand) {
    this._carname = brand;
  }
  get carname() {
    return this._carname;
  }
  set carname(x) {
    this._carname = x;
  }
}

const myCar = new Car("Ford");
myCar.carname = "Volvo"; # To set the carname
console.log(myCar.carname); # TO get the carname

# Hoisting in class

# Unlike functions, and other JavaScript declarations, class declarations are not hoisted.
# That means that you must declare a class before you can use it else will give error

2. ==> JavaScript Static Methods
# You cannot call a static method on an object, only on an object class.
# If you want to use the myCar object inside the static method, you can send it as a parameter:
class Car {
  constructor(name) {
    this.name = name;
  }
  static hello() {
    return "Hello!!";
  }
}

const myCar = new Car("Ford");
console.log( Car.hello()); # ERROR
console.log(Car.hello(myCar));
# console.log(myCar.hello()); #-> This will give an error
```

- JavaScript Callbacks
  - A callback is a function passed as an argument to another function

```bash
# Where callbacks really shine are in asynchronous functions, where one function has to wait for another function (like waiting for a file to load).

# Example-1
function calculate(x, y, fn) {
  const a = x + y;
  fn(a);
}
function display(result) {
  console.log(result);
}
calculate(3, 4, display); # display is a callback function

# Example-2
const myNumbers = [4, 1, -20, -7, 5, 9, -6];
function removeNegative(arr, callback) {
  const myarr = [];
  for (let num of arr) {
    if (callback(num)) {
      myarr.push(num);
    }
  }
  return myarr;
}
const result = removeNegative(myNumbers, (x) => x >= 0);
console.log(result);

# Example-3
function callbackFunction(name) {
  console.log("Hello " + name);
}

function outerFunction(callback) {
  let name = prompt("Please enter your name.");
  callback(name);
}

outerFunction(callbackFunction);

-- CALLBACK HELL
# Callback Hell is an anti-pattern with multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell looks like below,
async1(function(){
    async2(function(){
        async3(function(){
            async4(function(){
                ....
            });
        });
    });
});
```

- Asynchronous JavaScript => ("I will finish later!")
  - Functions running in parallel with other functions are called asynchronous
  - eg. setTimeout()

CALLBACK VS PROMISE VS ASYNC/AWAIT -> SAME EXAMPLES

```bash
https://www.freecodecamp.org/news/javascript-asynchronous-operations-in-the-browser/
# BELOW EXECUTIONS TAKES PLACE INSIDE JS RUNTIME
callstack (inside js engine) -> webapi -> callback/event queue -> event loop

# JS ENVIRONMENT
The JavaScript runtime is the environment that contains all the resources necessary for the execution of a JavaScript program. It includes the JavaScript Engine but also includes other things we will look at.

# JS ENGINE
For a browser to interpret JavaScript code, it needs to have a JavaScript engine. This JavaScript engine is a software component of a modern web browser that accepts JavaScript code, analyzes it, and transforms it into instructions the device will understand.

Different browsers today use different JavaScript engines. For example, the Chrome Browser uses the V8 Engine from Google, Firefox uses one called Spidermonkey,etc.

# CALL STACK
The call stack is a component of a JavaScript Engine that keeps track of all the functions the program executes.
Last In First Out (LIFO) is a term that summarizes how the call stack works. The last operation that went in is the first operation that will leave the stack.

# EXAMPLE
function greeting() {
	console.log("Hello World")
}
function run() {
	greeting()
}
run()
# HERE first run() -> greeting() -> console.log("Hello World") is executed
# SO THE LAST OPERATION IS EXECUTED FIRST (ie. console.log("Hello World") then> greeting() and then> run())

# WEB APIS
JavaScript uses the browser’s provided Web Application Programming Interfaces (Web APIs).
The Web APIs are a set of functions provided by the browser that the JavaScript engine can utilize. They include examples such as Document Object Model (DOM) manipulation methods, fetch, setInterval, setTimeout, promises, async-await functions, and more.
- IN NODEJS JS OFFLOAD OPERATION TO THE SYSTEMS KERNAL (MOST KERNAL ARE MULTITHREAD SO THEY CAN HANDLE IN THE BACKGROUND)
- The JavaScript Engine interacting with the Web APIs inside the JavaScript Runtime

# CALLBACK
Asynchronous operations provide a response after being processed using Web APIs. The purpose of writing an asynchronous function is to utilize the function''s output for subsequent operations. We refer to the functions that rely on the response from asynchronous operations as callback functions.

`A callback function is a function that is passed as an argument to a parent function, which the parent function needs to invoke after completing its process. In JavaScript, asynchronous operations utilize callbacks to further process the responses they receive from Web APIs.`

To ""recap"", a callback function is passed in as an argument to an asynchronous function and only runs when the asynchronous operation has been completed.

# EXAMPLE
fetch("<https://jsonplaceholder.typicode.com/users>")
.then((response) => response.json())
.then((response) => console.log(response))
# Here, the 1st "then" function will be executed after the response from fetch.
# And 2nd "then" function will be executed after the 1st "then" (another asyn function)

# CALLBACK QUEUE
The callback queue is a software mechanism that stores callback functions to be run after the Web APIs have processed asynchronous functions. It uses the queue data structure which works with the First In First Out (FIFO) approach. This means that the first callback added to that queue is going to be the first callback to leave.

- The JavaScript Engine interacting with the Web APIs AND AFTER THEIR EXECUTION THEY PUSH CALLBACK TO THE CALLBACK QUEUE, EVERTHING HAPPENS inside the JavaScript Runtime

# EVENT LOOP
The event loop is a loop that continuously checks if the call stack is empty. When the call stack is not empty, it allows the ongoing process to continue. But when the call stack becomes empty, the event loop fetches the task at the top of the callback queue and adds it to the call stack.
So the JavaScript Engine executes callbacks only after everything in the call stack has been processed.

# EXAMPLE
console.log('A')
setTimeout(( ) => console.log('B'), 0) # THIS WILL BE EXECUTED AT LAST
console.log('C')
// A
// C
// B

```

```bash

console.log("1"); # first this will be printed
setTimeout(( ) => console.log("I will"), 2000);  # third(Last) this will be printed
console.log("2"); # second this will be printed
# 1, 2, I will #

# Callback Alternatives
    # With asynchronous programming, JavaScript programs can start long-running tasks, and continue running other tasks in parallel.
    # But, asynchronus programmes are difficult to write and difficult to debug.
    # Because of this, most modern asynchronous JavaScript methods don't use callbacks. Instead, in JavaScript, asynchronous programming is solved using Promises instead.

```

- JavaScript Promises
  - "Producing code" is code that can take some time
  - "Consuming code" is code that must wait for the result
  - A Promise is an Object that links Producing code and Consuming code

```bash
# Promise Syntax

let myPromise = new Promise((res, rej) => {
  # "Producing Code" (May take some time) --> It can be anything like api call
  const x = 0;
  if (x === 0) {
    res();
  } else {
    rej();
  }
});
console.log(myPromise); # Promise { undefined }

# "Consuming Code" (Must wait for a fulfilled Promise)
# first callback is for success and second callback is for failure ### Both are optional, so you can add a callback for success or failure only.
myPromise.then(
  () => console.log("resolve"),
  () => console.log("reject")
);

-> A JavaScript Promise object can be: (myPromise.state -- myPromise.result)
    # Pending -- the result is undefined
    # Fulfilled -- then the result is a value.
    # Rejected -- then the result is an error object.
# You cannot access the Promise properties state and result.
# You must use a Promise method to handle promises. (myPromise.then().catch()..)

#--> PROMISE VS CALLBACK

# CALLBACK
setTimeout(() => myFunction("I love You !!!"), 2000);
const myFunction = (value) => { ####### HOW THIS DON'T GIVE ERROR AS IT IS CALLED ABOVE IT
  console.log(value);
};

# PROMISE
let myPromise = new Promise((myResolve, myReject) => {
  setTimeout(() => myResolve("I love You !!"), 3000);
});
myPromise.then((value) => console.log(value));

-- promise chaining
# The process of executing a sequence of asynchronous tasks one after another using promises is known as Promise chaining.
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000);
})
  .then(function (result) {
    console.log(result); // 1
    return result * 2;
  })
  .then(function (result) {
    console.log(result); // 2
    return result * 3;
  })
  .then(function (result) {
    console.log(result); // 6
    return result * 4;
  });

-- promise.all
# Promise.all is a promise that takes an array of promises as an input (an iterable), and it gets resolved when all the promises get resolved or any one of them gets rejected.
Promise.all([Promise1, Promise2, Promise3])
  .then((result) => console.log(result))
  .catch((error) => console.log(`Error in promises ${error}`));

-- Promise.race()
# This method will return the promise instance which is firstly resolved or rejected.
var promise1 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 500, "one");
});
var promise2 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "two");
});
Promise.race([promise1, promise2]).then(function (value) {
  console.log(value); // "two" // Both promises will resolve, but promise2 is faster
});
```

- JavaScript Async - ("async and await make promises easier to write")
  - async makes a function return a Promise
  - await makes a function wait for a Promise

```bash
# ASYNC SYNTAX:-> Both function works the same way
async function myFunction() {
  return "Hello!!";
}
function myFunction() {
  return new Promise((res, rej) => res("Hello2"));
}
myFunction().then(
  () => console.log(myFunction()),
  () => console.log("reject")
);

# AWAIT SYNTAX:->
async function myFunction() {
  let myPromise = new Promise((res) => setTimeout(() => res("Hello!"), 2000));
  console.log(myPromise); // Promise { <pending> }
  const value = await myPromise;
  console.log(value); // Hello!
  console.log(myPromise); // Promise { 'Hello!' }
}
myFunction();

async function func() {
  return 10;
}
console.log( func());                         # Promise { 10 } |  Promise {<fulfilled>: 10}

#
async function delayedLog(item) {
  await new Promise((resolve) => setTimeout(resolve, 2000));
  console.log(item);
}

# WITH FOREACH CODE
  # - array.forEach does not wait for await delayedLog(item) to complete before starting the next iteration.
  # - All iterations start almost immediately and the delayedLog function is called concurrently for each item.
  # - "Process completed!" is logged before any of the delayedLog operations have completed, because forEach itself is not asynchronous and does not wait for the async function to resolve.
// async function processArray(array) {
//   array.forEach(async(item) => {
//     await delayedLog(item);
//   })
// }
# UNCOMMENT ABOVE PART AND COMMENT THIS (BELOW WILL WAIT EVERY 2 SECOND ABOVE WON'T)

# WITH FOR-OF CODE
  # - Each delayedLog(item) waits for 2 seconds before logging the item.
  # - The next iteration starts only after the previous one has completed, leading to sequential execution.
  # - The total time taken will be 2 seconds * number of items in the array.
async function processArray(array) {
  for (const item of array) {
    await delayedLog(item);
  }
  console.log("Process completed!"); # THIS WILL BE PRINTED 1ST OR LAST DEPENDING ON COMMENT
}

processArray([1, 2, 3, 4]);


```

- JavaScript HTML DOM

```bash
- When a web page is loaded, the browser creates a Document Object Model of the page.
- The HTML DOM is a standard object model and programming interface for HTML

<input type="text" id="fname" oninput="upperCase()"> # This will change every input to uppercase

# Event Bubbling or Event Capturing

# In bubbling the inner most element's event is handled first and then the outer: the <p> element's click event is handled first, then the <div> element's click event.

# In capturing the outer most element's event is handled first and then the inner: the <div> element's click event will be handled first, then the <p> element's click event.

# The default value is false, which will use the bubbling propagation, when the value is set to true, the event uses the capturing propagation.

addEventListener("click", myFunction, true);
removeEventListener("mousemove", myFunction);

---- The Browser Object Model
1. JS window
2. JS screen
3. JS location
4. JS history
5. JS navigator
6. JS popup alert
7. JS timing
8. JS cookies

1. JS window # All global JavaScript objects, functions, and variables automatically become members of the window object.

window.innerHeight - the inner height of the browser window (in pixels)
window.innerWidth - the inner width of the browser window (in pixels)
window.open() - open a new window
window.close() - close the current window
window.moveTo() - move the current window
window.resizeTo() - resize the current window

2. JS screen # The window.screen object contains information about the user's screen.

screen.width
screen.height
screen.availWidth
screen.availHeight
screen.colorDepth
screen.pixelDepth

3. JS location # The window.location object can be used to get the current page address (URL) and to redirect the browser to a new page.

window.location.href returns the href (URL) of the current page
window.location.hostname returns the domain name of the web host
window.location.pathname returns the path and filename of the current page
window.location.protocol returns the web protocol used (http: or https:)
window.location.assign() loads a new document

4. JS history # The window.history object contains the browsers history.

history.back() - same as clicking back in the browser
history.forward() - same as clicking forward in the browser

5. JS navigator # The window.navigator object contains information about the visitor's browser.

navigator.cookieEnabled
navigator.appCodeName
navigator.platform

6. JS popup alert

window.alert() :==> alert("I am an alert box!");
# An alert box is often used if you want to make sure information comes through to the user.
# When an alert box pops up, the user will have to click "OK" to proceed.

window.confirm() :==> confirm("Press a button!")
# A confirm box is often used if you want the user to verify or accept something.
# When a confirm box pops up, the user will have to click either "OK" or "Cancel" to proceed.
# If the user clicks "OK", the box returns true. If the user clicks "Cancel", the box returns false.

window.prompt() :==> prompt("Please enter your name", "Harry Potter")
# A prompt box is often used if you want the user to input a value before entering a page.
# When a prompt box pops up, the user will have to click either "OK" or "Cancel" to proceed after entering an input value.
# If the user clicks "OK" the box returns the input value. If the user clicks "Cancel" the box returns null.
# Can give default value as second argument (eg. Harry Potter)


7. JS timing

setTimeout(function, milliseconds) # Executes a function, after waiting a specified ms.
setInterval(function, milliseconds) # repeats the execution of the function continuously.
clearTimeout(variable) # stops the executions of the function specified in the setTimeout() method.
clearInterval(variable) # stops the executions of the function specified in the setInterval() method.
# you can technically use clearTimeout() and clearInterval() interchangeably. However, for clarity, you should avoid doing so.
# eg. const x = setTimeout(function, milliseconds); then-> clearTimeout(x)

const arr = [1, 2, 3, 4, 5];
arr.forEach((i) => setTimeout(() => console.log(i), 1000));
# It will print 1,2,3,4,5 all together after 1 second: Because setTimeout will await the first array then it will go to second iteration same will work till all the iteration then after 1 sec all start to log value


8. JS cookies # Cookies let you store user information in web pages.
# Cookies are data, stored in small text files, on your computer.
# By default, the cookie is deleted when the browser is closed

document.cookie # it can create, read, and delete cookies

# create a cookie or change it
document.cookie = "username=John Doe";
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/"; # You can also add an expiry date (in UTC time) and path for cookie to store
# Read a Cookie
let x = document.cookie;
# Delete a Cookie -- Just set the expires parameter to a past date
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;"; # You should define the cookie path to ensure that you delete the right cookie.

```

- Web APIs

```bash
# The Web Storage API is a simple syntax for storing and retrieving data in the browser.
localStorage.setItem("name", "John Doe");
localStorage.getItem("name"); # returns "John Doe"

# The sessionStorage Object
# Same as localStorage only difference is sessionStorage object stores data for one session.
sessionStorage.setItem("name", "John Doe");
sessionStorage.getItem("name");

key(n)	                Returns the name of the nth key in the storage
length	                Returns the number of data items stored in the Storage object
getItem(keyname)	      Returns the value of the specified key name
setItem(keyname, value)	Adds a key to the storage, or updates a key value (if already exists)
removeItem(keyname)	    Removes that key from the storage
clear()	                Empty all key out of the storage


# JavaScript Fetch API

async function getText(file) {
  let myObject = await fetch(file);
  let myText = await myObject.text();
  myDisplay(myText);
}

# Web Geolocation API
# The HTML Geolocation API is used to get the geographical position of a user.
# The Geolocation API will only work on secure contexts such as HTTPS.

getCurrentPosition(); # method is used to return the user's position.

# COPY THIS AND PASTE IT TO THE CONSOLE OF THE BROWSER
function getLocation() {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(showPosition);
  } else {
    console.log("Geolocation is not supported by this browser.");
  }
}
function showPosition(position) {
  console.log(position);
  console.log(position.coords);
}
getLocation();

# Handling Errors and Rejections
function showError(error) {
  switch(error.code) {
    case error.PERMISSION_DENIED:
      x.innerHTML = "User denied the request for Geolocation."
      break;
    case error.POSITION_UNAVAILABLE:
      x.innerHTML = "Location information is unavailable."
      break;
    case error.TIMEOUT:
      x.innerHTML = "The request to get user location timed out."
      break;
    case error.UNKNOWN_ERROR:
      x.innerHTML = "An unknown error occurred."
      break;
  }
}

# To display the result in a map, you need access to a map service, like Google Maps.

# the returned latitude and longitude is used to show the location in a Google Map (using a static image):
function showPosition(position) {
  let latlon = position.coords.latitude + "," + position.coords.longitude;

  let img_url = "https://maps.googleapis.com/maps/api/staticmap?center=
  "+latlon+"&zoom=14&size=400x300&sensor=false&key=YOUR_KEY";

  document.getElementById("mapholder").innerHTML = "<img src='"+img_url+"'>";
}

# Geolocation Object

watchPosition(); # Returns the current position of the user and continues to return updated position as the user moves (like the GPS in a car).
clearWatch(); # Stops the watchPosition() method.
```

- AJAX = Asynchronous JavaScript And XML. ---> IT'S LIKE FETCH REQUEST FROM BROWSER

  - Read data from a web server - after the page has loaded
  - Update a web page without reloading the page
  - Send data to a web server - in the background
  - AJAX is not a programming language.
  - AJAX is a technique for accessing web servers from a web page.
  - AJAX just uses a combination of:

    - A browser built-in XMLHttpRequest object (to request data from a web server)
    - JavaScript and HTML DOM (to display or use the data)

  - The Fetch API interface allows web browser to make HTTP requests to web servers.
  - If you use the XMLHttpRequest Object, Fetch can do the same in a simpler way.

```bash

```

- JSON stands for JavaScript Object Notation
- JSON is a text format for storing and transporting data

  - The file type for JSON files is ".json"
  - The MIME type for JSON text is "application/json"

```bash
# In JSON, values must be one of the following data types:

1. a string

- {"name":"John"}

2. a number

- {"age":30}

3. an object

- { "employee":{"name":"John", "age":30, "city":"New York"} }
4. an array

- { "employees":["John", "Anna", "Peter"] }

5. a boolean

- {"sale":true}

6. null

- {"middlename":null}

# CANNOT SEND THIS 3 ITEMS OVER JSON
  - a date
  - undefined
  - function

  # - [IF YOU SEND RAW FUNCTION THEN IT WILL AUTOMATICALLY BE REMOVED]
const obj = {name: "John", age: function () {return 30;}, city: "New York"};
const myJSON = JSON.stringify(obj); # {"name":"John","city":"New York"} - fn is removed

  # Stringify Functions - YOU CAN SEND THE FUNCTION BY FIRST CONVERTING IT INTO STRING?
  # [ AVOID THIS TRICK AND DONT SEND FUNCTION OVER JSON ]
  # If you need to include a function, write it as a string.
  # then use eval() to convert them back into functions.

console.log( JSON.stringify({ myArray: ["one", undefined, function () {}, Symbol("")] }));
# {"myArray":["one",null,null,null]}
console.log( JSON.stringify({ [Symbol.for("one")]: "one" }, [Symbol.for("one")]));
# {}


# JSON vs XML

#  JSON is Better Than XML
XML is much more difficult to parse than JSON.
JSON is parsed into a ready-to-use JavaScript object.

->> JSON.parse(val,fun) # to convert text into a JavaScript object: function is called reviver and is optional
# The reviver parameter is a function that checks each property, before returning the value.
const text = '{"name":"John", "birth":"1986-12-14", "city":"New York"}';
const obj = JSON.parse(text, function (key, value) {
  if (key == "birth") {
    return new Date(value);
  } else {
    return value;
  }
 });  # Here the if the value of birth will be changed to date and not returned as string
console.log(obj); # { name: 'John', birth: 1986-12-14T00:00:00.000Z, city: 'New York' }

->> JSON.stringify(); # to convert it into a string.
# eg
const obj = {name: "John", age: 30, city: "New York"};
const myJSON = JSON.stringify(obj);

# Storing Data
# Use JSON to store data to local storage in browser

# JSON.stringify() function will convert any dates into strings.
# You can convert the string back into a date object at the receiver.

```

callback and promise: difference + similarity, write same examples in both

- encoding and decoding a URL
  - Use encodeURIComponent when you need to encode a single part of a URI, such as a query parameter.
  - Use encodeURI when you need to encode a full URL.
  - Use decodeURIComponent to decode a single encoded component.
  - Use decodeURI to decode an entire encoded URL.

```bash

# Encoding
# 1. encodeURIComponent()
const urlComponent = 'Hello World!';
const encodedComponent = encodeURIComponent(urlComponent);
console.log(encodedComponent); # Output: Hello%20World%21

# 2. encodeURI()
const url = 'http://example.com/Hello World!';
const encodedURL = encodeURI(url);
console.log(encodedURL); # Output: http://example.com/Hello%20World!

# Decoding
# 3. decodeURIComponent()
const encodedComponent = 'Hello%20World%21';
const decodedComponent = decodeURIComponent(encodedComponent);
console.log(decodedComponent); # Output: Hello World!

# 4. decodeURI()
const encodedURL = 'http://example.com/Hello%20World!';
const decodedURL = decodeURI(encodedURL);
console.log(decodedURL); # Output: http://example.com/Hello World!

```

- All Info

- CODE ALMOST ALL THE QUESTION AND GIVE ANSWERS FOR THEM
- https://github.com/sudheerj/javascript-interview-questions?tab=readme-ov-file

```bash

1. Difference betweem-> local storage vs session storage vs cookie

https://github.com/sudheerj/javascript-interview-questions?tab=readme-ov-file#what-are-the-differences-between-cookie-local-storage-and-session-storage

2. What is the difference between native, host and user objects

Native objects are objects that are part of the JavaScript language defined by the ECMAScript specification. For example, String, Math, RegExp, Object, Function etc core objects defined in the ECMAScript spec. Host objects are objects provided by the browser or runtime environment (Node). For example, window, XmlHttpRequest, DOM nodes etc are considered as host objects. User objects are objects defined in the javascript code. For example, User objects created for profile information.

3. What is the use of preventDefault method

The preventDefault() method cancels the event if it is cancelable, meaning that the default action or behaviour that belongs to the event will not occur. For example, prevent form submission when clicking on submit button and prevent opening the page URL when clicking on hyperlink are some common use cases.
Note: Remember that not all events are cancelable.

4. What is BOM

The Browser Object Model (BOM) allows JavaScript to "talk to" the browser. It consists of the objects navigator, history, screen, location and document which are children of the window. The Browser Object Model is not standardized and can change based on different browsers.

5. What is ECMAScript

ECMAScript is the scripting language that forms the basis of JavaScript. ECMAScript standardized by the ECMA International standards organization in the ECMA-262 and ECMA-402 specifications. The first edition of ECMAScript was released in 1997.

6. How do you check if a key exists in an object

- Using in operator:
"key" in obj; # true if exist
!("key" in obj); # true if not exist

- Using hasOwnProperty method:
obj.hasOwnProperty("key"); // true

- Using undefined comparison:
const user = {
  name: "John",
};
console.log(user.name !== undefined); // true
console.log(user.nickName !== undefined); // false

7. How do you test for an empty object

# Since date object length is 0, you need to check constructor check as well
Object.keys(obj).length === 0 && obj.constructor === Object;
Object.entries(obj).length === 0 && obj.constructor === Object;

8. Can we define properties for functions (140)
# Yes, We can define properties for functions because functions are also objects.
fn = function (x) {
  #Function code goes here
};
fn.name = "John";

fn.profile = function (y) {
  #Profile code goes here
};

9. What is the way to find the number of parameters expected by a function
# You can use function.length syntax to find the number of parameters expected by a function. Let's take an example of sum function to calculate the sum of numbers,
function sum(num1, num2, num3, num4) {
  return num1 + num2 + num3 + num4;
}
sum.length; // 4 is the number of parameters expected.

10. What is tree shaking

Tree shaking is a form of dead code elimination. It means that unused modules will not be included in the bundle during the build process and for that it relies on the static structure of ES2015 module syntax,( i.e. import and export).
Tree shaking is implemented in Rollup and Webpack bundlers.

11. Is it recommended to use eval

No, it allows arbitrary code to be run which causes a security problem. As we know that the eval() function is used to run text as code. In most of the cases, it should not be necessary to use it.

12. What is the difference between proto and prototype

https://github.com/sudheerj/javascript-interview-questions?tab=readme-ov-file#what-is-the-difference-between-proto-and-prototype

13. Spread operator vs Rest operator

# SPREAD OPERATOR
The spread operator, denoted by three consecutive dots (...), is primarily used for expanding iterables like arrays into individual elements. This operator allows us to efficiently merge, copy, or pass array elements to functions without explicitly iterating through them.
# Example
const arr1 = [1, 2];
const arr2 = [3, 4];
console.log(...arr1, ...arr2); # 1, 2, 3, 4
console.log([...arr1, ...arr2]); # [ 1, 2, 3, 4 ]

# REST OPERATOR
While the spread operator expands elements, the rest operator(rest parameter) condenses them into a single entity within function parameters or array destructuring.
# Example1 -- function parameters
function sum(a, ...b) {
  console.log({ a, b }); # { a: 1, b: [ 2, 3 ] }
}
sum(1, 2, 3);

# Example2 -- array destructuring
const [a, b, ...c] = [1, 2, 3, 4, 5];
console.log(a, b, c); # 1, 2, [ 3, 4, 5 ]

A rest parameter must be last in a parameter list, as its job is to collect all the remaining arguments into an array.
# Example
const [a, b, ...c, e] = [1, 2, 3, 4, 5]; # GIVES ERROR

# DIFFERENCE
The main difference between rest and spread is that the rest operator puts the rest of some specific user-supplied values into a JavaScript array. But the spread syntax expands iterables into individual elements.

# Example
function sum(a, ...b) { # REST OPERATOR
  console.log({ a, b }); // { a: 1, b: [ 2, 3, 4 ] }
}

const arr1 = [1, 2];
const arr2 = [3, 4];

sum(...arr1, ...arr2); // 1, 2, 3, 4 # SPREAD OPERATOR

14. What is the purpose of using object is method

# Example
Object.is("hello", "hello"); // true
Object.is(window, window); // true
Object.is([], []); // false

Some of the applications of Object''s is method are follows,
  It is used for comparison of two strings.
  It is used for comparison of two numbers.
  It is used for comparing the polarity of two numbers.
  It is used for comparison of two objects.

15. How do you print the contents of web page

The window object provided a print() method which is used to print the contents of the current window. It opens a Print dialog box which lets you choose between various printing options.

16. What is an anonymous function

An anonymous function is a function without a name! Anonymous functions are commonly assigned to a variable name or used as a callback function.

17. What are the advantages of Getters and Setters

They provide simpler syntax
They are used for defining computed properties, or accessors in JS.
Useful to provide equivalence relation between properties and methods
They can provide better data quality
Useful for doing things behind the scenes with the encapsulated logic.

18. What is an event loop

The event loop is a process that continuously monitors both the call stack and the event queue and checks whether or not the call stack is empty. If the call stack is empty and there are pending events in the event queue, the event loop dequeues the event from the event queue and pushes it to the call stack. The call stack executes the event, and any additional events generated during the execution are added to the end of the event queue.
Note: The event loop allows Node.js to perform non-blocking I/O operations, even though JavaScript is single-threaded, by offloading operations to the system kernel whenever possible. Since most modern kernels are multi-threaded, they can handle multiple operations executing in the background.

19. What is call stack

Call Stack is a data structure for javascript interpreters to keep track of function calls(creates execution context) in the program. It has two major actions,
  - Whenever you call a function for its execution, you are pushing it to the stack.
  - Whenever the execution is completed, the function is popped out of the stack.

20. What is an event queue -> [ WHOLE ASYNC FUNCTION STRUCTURE ]

The event queue follows the queue data structure. It stores async callbacks to be added to the call stack. It is also known as the Callback Queue or Macrotask Queue.

Whenever the call stack receives an async function, it is moved into the Web API. Based on the function, Web API executes it and awaits the result. Once it is finished, it moves the callback into the event queue (the callback of the promise is moved into the microtask queue).

The event loop constantly checks whether or not the call stack is empty. Once the call stack is empty and there is a callback in the event queue, the event loop moves the callback into the call stack. But if there is a callback in the microtask queue as well, it is moved first. The microtask queue has a higher priority than the event queue.

21. What is an Unary operator

The unary(+) operator is used to convert a variable to a number.If the variable cannot be converted, it will still become a number but with the value NaN. Let''s see this behavior in an action.

var x = "100";
var y = +x;
console.log(typeof x, typeof y); // string, number

var a = "Hello";
var b = +a;
console.log(typeof a, typeof b, b); // string, number, NaN

22. How do you define multiple properties on an object

The Object.defineProperties() method is used to define new or modify existing properties directly on an object and returning the object. Let''s define multiple properties on an empty object,

const newObject = {};
Object.defineProperties(newObject, {
  newProperty1: {
    value: "John",
    writable: true,
  },
  newProperty2: {},
});

23. What is an enum

An enum is a type restricting variables to one value from a predefined set of constants. JavaScript has no enums but typescript provides built-in enum support.

24. How do you list all properties of an object

You can use the Object.getOwnPropertyNames() method which returns an array of all properties found directly in a given object. Let''s see the usage of this in an example below:

const newObject = { a: 1, b: 2, c: 3 };

console.log( Object.getOwnPropertyNames(newObject));
["a", "b", "c"];

25. How do you compare scalar arrays

You can use length and every method of arrays to compare two scalar(compared directly using ===) arrays. The combination of these expressions can give the expected result,

const arrayFirst = [1, 2, 3, 4, 5];
const arraySecond = [1, 2, 3, 4, 5];
console.log(
  arrayFirst.length === arraySecond.length &&
    arrayFirst.every((value, index) => value === arraySecond[index])
); // true

If you would like to compare arrays irrespective of order then you should sort them before,

const arrayFirst = [2, 3, 1, 4, 5];
const arraySecond = [1, 2, 3, 4, 5];
console.log(
  arrayFirst.length === arraySecond.length &&
    arrayFirst.sort().every((value, index) => value === arraySecond[index])
); //true

26. How do you create an infinite loop

You can create infinite loops using for and while loops without using any expressions. The for loop construct or syntax is better approach in terms of ESLint and code optimizer tools,

for (;;) {}
while (true) {}

27. Can I redeclare let and const variables

No, you cannot redeclare let and const variables. If you do, it throws below error

Explanation: The variable declaration with var keyword refers to a function scope and the variable is treated as if it were declared at the top of the enclosing scope due to hoisting feature. So all the multiple declarations contributing to the same hoisted variable without any error. Let''s take an example of re-declaring variables in the same scope for both var and let/const variables.

var name = "John";
function myFunc() {
  var name = "Nick";
  var name = "Abraham"; // Re-assigned in the same function block
  alert(name); // Abraham
}
myFunc();
alert(name); // John

--- The block-scoped multi-declaration throws syntax error,

let name = "John";
function myFunc() {
  let name = "Nick";
  let name = "Abraham"; // Uncaught SyntaxError: Identifier 'name' has already been declared
  alert(name);
}
myFunc();
alert(name);

28. Does the const variable make the value immutable

No, the const variable doesn't make the value immutable. But it disallows subsequent assignments(i.e, You can declare with assignment but can't assign another value later)

const userList = [];
userList.push("John"); // Can mutate even though it can''t re-assign
console.log(userList); // ['John']

29. What are typed arrays -- 320

Typed arrays are array-like objects from ECMAScript 6 API for handling binary data.

30. What is postMessage()?

The method window. postMessage() is used by the application to allow cross-origin communication between different window objects, e.g. between a page and a pop-up that it spawned or between a page and an iframe embedded within it.

31. Is JavaScript faster than server side script

Yes, JavaScript is faster than server side scripts. Because JavaScript is a client-side script it does not require any web server’s help for its computation or calculation. So JavaScript is always faster than any server-side script like ASP, PHP, etc

32. What is the difference between Shallow and Deep copy

Shallow Copy: Shallow copy is a bitwise copy of an object. A new object is created that has an exact copy of the values in the original object. If any of the fields of the object are references to other objects, just the reference addresses are copied i.e., only the memory address is copied.

Deep copy: A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.

33. What happens if we add two arrays

If you add two arrays together, it will convert them both to strings and concatenate them. For example, the result of adding arrays would be as below,
As per JavaScript coercion rules, the addition of arrays together will toString them: [] + [] === ""

console.log(["a"] + ["b"]); // "ab"
console.log([] + []); // ""

34. How do you remove falsy values from an array

const myArray = [false, null, 1, 5, undefined];
const trueArray = myArray.filter((v) => !!v);  # [1, 5]
const trueArray = myArray.filter((v) => v);    # [1, 5]
const trueArray = myArray.filter(Boolean);     # [1, 5]
console.log({ trueArray });

35. How do you get unique values of an array

const myArray = [1, 2, 3, 2, 1];
const uniqueArray = [...new Set(myArray)]; // [ 1, 2, 3 ]

36. How do you empty an array

let cities = ["Singapore", "Delhi", "London"];
cities.length = 0; // cities becomes []

37. What is the easiest way to convert an array to an object

var fruits = ["banana", "apple", "orange", "watermelon"];
var fruitsObject = { ...fruits };
console.log(fruitsObject); // {0: "banana", 1: "apple", 2: "orange", 3: "watermelon"}

--  YOU CAN ALSO RESIZE AN ARRAY
var array = [1, 2, 3, 4, 5];
console.log(array.length); // 5

array.length = 2;
console.log(array.length); // 2
console.log(array); // [1,2]

38. How do you create an array with some data

var newArray = new Array(5).fill("0");
console.log(newArray); // ["0", "0", "0", "0", "0"]

39. How do you display data in a tabular format using console object

The console.table() is used to display data in the console in a tabular format to visualize complex arrays or objects.

40. How do you disable right click in the web page

The right click on the page can be disabled by returning false from the oncontextmenu attribute on the body element.

<body oncontextmenu="return false;"></body>

41. What is AJAX

AJAX stands for Asynchronous JavaScript and XML. We can send data to the server and get data from the server without reloading the web page.

42. What is heap

Heap(Or memory heap) is the memory location where objects are stored when we define variables. i.e, This is the place where all the memory allocations and de-allocation take place. Both heap and call-stack are two containers of JS runtime. Whenever runtime comes across variables and function declarations in the code it stores them in the Heap.

43. What is babel

Babel is a JavaScript transpiler to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments.

44. What is the difference between function and class declarations

The main difference between function declarations and class declarations is hoisting. The function declarations are hoisted but not class declarations.

45. What are the differences between arguments object and rest parameter

There are three main differences between arguments object and rest parameters
  - The arguments object is an array-like but not an array. Whereas the rest parameters are array instances.
  - The arguments object does not support methods such as sort, map, forEach, or pop. Whereas these methods can be used in rest parameters.
  - The rest parameters are only the ones that haven’t been given a separate name, while the arguments object contains all arguments passed to the function

46. What is the difference between isNaN and Number.isNaN?

isNaN: The global function isNaN converts the argument to a Number and returns true if the resulting value is NaN.
Number.isNaN: This method does not convert the argument. But it returns true when the type is a Number and value is NaN.
# Example
isNaN("hello");   // true
Number.isNaN("hello"); // false
isNaN("100");   // false
Number.isNaN("100"); // false
isNaN("NaN"); // true
Number.isNaN("NaN"); // false
isNaN(NaN); // true
Number.isNaN(NaN); // true
Number.isNaN("ABC" / "ABC"); // true
Number.isNaN("ABC" * "ABC"); // true

# isNaN converts the argument to a Number and returns true if the resulting value is NaN.
# Number.isNaN does not convert the argument; it returns true when the argument is a Number and is NaN.

|               |       Number.isNaN()       |        isNaN()
----------------+----------------------------+-----------------------
value           | value is a Number | result | Number(value) | result
----------------+-------------------+--------+---------------+-------
undefined       | false             | false  | NaN           | true
{}              | false             | false  | NaN           | true
"blabla"        | false             | false  | NaN           | true
new Date("!")   | false             | false  | NaN           | true
new Number(0/0) | false             | false  | NaN           | true
"ABC" * "ABC"   | true              | true   | NaN           | true
# IF STRING OR OBJECTS,ETC (IF NOT NUMBER)

47. How do you reverse an array without modifying original array?

The reverse() method reverses the order of the elements in an array but it mutates the original array. Let''s take a simple example to demonistrate this case,

# MODIFYING ORIGINAL ARRAY
const originalArray = [1, 2, 3, 4, 5];
const newArray = originalArray.reverse();
console.log(newArray); // [ 5, 4, 3, 2, 1]
console.log(originalArray); // [ 5, 4, 3, 2, 1]

# WITHOUT MODIFYING ORIGINAL ARRAY

# 1. Using slice and reverse methods: In this case, just invoke the slice() method on the array to create a shallow copy followed by reverse() method call on the copy.
const originalArray = [1, 2, 3, 4, 5];
const newArray = originalArray.slice().reverse(); //Slice an array gives a new copy
console.log(originalArray); // [1, 2, 3, 4, 5]
console.log(newArray); // [ 5, 4, 3, 2, 1]

# 2. Using spread and reverse methods: In this case, let's use the spread syntax (...) to create a copy of the array followed by reverse() method call on the copy.
const originalArray = [1, 2, 3, 4, 5];
const newArray = [...originalArray].reverse();
console.log(originalArray); // [1, 2, 3, 4, 5]
console.log(newArray); // [ 5, 4, 3, 2, 1]

48. What is debouncing?

Debouncing is a programming pattern that allows delaying execution of some piece of code until a specified time to avoid unnecessary CPU cycles, API calls and improve performance. The debounce function make sure that your code is only triggered once per user input. The common usecases are Search box suggestions, text-field auto-saves, and eliminating double-button clicks.

# DEBOUNCING USING CLOSURE
const debounceFn = (() => {
  let value;
  return (val) => {
    clearTimeout(value);
    value = setTimeout(() => console.log("Called", val), 1000);
  };
})();
debounceFn(1); # This will not execute (Override by second function)
setTimeout(( ) => debounceFn(2), 500); # This will be executed

# DEBOUNCING WITHOUT USING CLOSURE
let value;
function debounceFn(val) {
  clearTimeout(value);
  value = setTimeout(() => console.log("Called", val), 1000);
}
debounceFn(1);
setTimeout(() => debounceFn(2), 500);

49. What is Throttling?

Throttling is a technique used to limit the rate at which a function is called. Throttling transforms a function such that it can only be called once in a specific interval of time.

# EXAMPLE









50. What is optional chaining?

The ?. operator is like the . chaining operator, except that instead of causing an error if a reference is nullish (null or undefined), the expression short-circuits with a return value of undefined. When used with function calls, it returns undefined if the given function does not exist.
# EX1
const adventurer = {
  name: "Alice",
  cat: {
    name: "Dinah",
  },
};
const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

# EX2
console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined

51. How to verify if a variable is an array?

It is possible to check if a variable is an array instance using 3 different ways,
  # 1. Array.isArray() method:
  Array.isArray(myArr); // true
  # 2. instanceof operator:
  myArr instanceof Array; // true
  # 3. Checking constructor type:
  myArr.constructor === Array; // true

52. What is pass by value and pass by reference?

Pass-by-value creates a new space in memory and makes a copy of a value. Primitives such as string, number, boolean etc will actually create a new copy. Hence, updating one value doesn''t impact the other value. i.e, The values are independent of each other.

Pass-by-reference doesn''t create a new space in memory but the new variable adopts a memory address of an initial variable. Non-primitives such as objects, arrays and functions gets the reference of the initiable variable. i.e, updating one value will impact the other variable.

# PRIMITIVES VS NON-PRIMITIVES
Primitives	                      Non-primitives
These types are predefined	      Created by developer
These are immutable	              Mutable
Compare by value	                Compare by reference
Stored in Stack	                  Stored in heap
Contain certain value	            Can contain NULL too

53. What is the difference between map and forEach functions?

Both map and forEach functions are used to iterate over an arrays but there are some differences in their functionality.
  I. Returning values: The map method returns a new array with transformed elements whereas forEach method returns undefined eventhough both of them are doing the same job.
  - The `forEach()` method in JavaScript always returns undefined. This is because forEach() is used to iterate over arrays and perform side effects on each element, rather than returning a `new array or transforming the original array`

  II. Chaining methods: The map method is chainable. i.e, It can be attached with reduce, filter, sort and other methods as well. Whereas forEach cannot be attached with any other methods because it returns undefined value.

  III. Mutation: The map method doesn't mutate the original array by returning new array. Whereas forEach method also doesn't mutate the original array but it's callback is allowed to mutate the original array.

```

- PRACTICE QUESTIONS (mostly difficult)

```bash

# 1 MAKE A FUNCTION ONLY RUNS ONCE (V.HARD)
function once(func, context) {
  let ran;

  return function () {
    if (func) {
      ran = func.apply(context || this, arguments);
      func = null;
    }
    return ran;
  };
}

const hello = once((a, b) => console.log("Hello", a, b));
const hello1 = once((a, b) => console.log("Hello", a, b));

hello(1, 2);
hello(1, 2);
hello(3, 2);
hello1(2, 3);
hello1(2, 3);

# 2 MEMOIZE THE FUNCTION RESULT (V.HARD)
function myMemoize(fn, context) {
  const res = {};
  return function (...args) {
    var argsCache = JSON.stringify(args);
    if (!res[argsCache]) {
      res[argsCache] = fn.call(context || this, ...args);
    }
    return res[argsCache];
  };
}

const clumsyProduct = (num1, num2) => {
  for (let i = 1; i <= 1000000; i++) {}
  return num1 * num2;
};

const memoizedclumzyProduct = myMemoize(clumsyProduct);

# HERE THE FUNCTION WILL RUN AND RESULT WILL BE SAVED
console.time("First Call");
console.log(memoizedclumzyProduct(9467, 7649));
console.timeEnd("First Call");

# HERE THE MEMOIZED RESULT WILL BE SHOWN
console.time("Second Call");
console.log(memoizedclumzyProduct(9467, 7649));
console.timeEnd("Second Call");

```

### Typescript:

-- ----- ALSO GET DATA FROM THE TS LECTURE NOTES FROM (DAILYCODE + CMS + MY_NOTES)

- TypeScript is JavaScript with added syntax for types.

- TypeScript uses compile time type checking. Which means it checks if the specified types match before running the code, not while running the code.

- TypeScript is transpiled into JavaScript using a compiler.

```bash
# Type Assignment ->
# 1. Explicit: writing out the type:
let firstName: string = "Dylan";

# 2. Implicit: TypeScript will "guess" the type, based on the assigned value:
let firstName = "Dylan";

# Note: Having TypeScript "guess" the type of a value is called infer.
# TypeScript may not always properly infer what the type of a variable may be.
#In such cases, it will set the type to any which disables type checking.
```

- TypeScript Simple Types

  - There are three main primitives in JavaScript and TypeScript.
    - boolean - true or false values
    - number - whole numbers and floating point values
    - string - text values like "TypeScript Rocks"
  - There are also 2 less common primitives used in later versions of Javascript and TypeScript.
    - bigint - whole numbers and floating point values, but allows larger negative and positive numbers than the number type.
    - symbol are used to create a globally unique identifier.

```bash

```

- TypeScript Special Types - [These types don't have much use]

  - any - it disables type checking and effectively allows all types to be used.

    - any can be a useful way to get past errors since it disables type checking, but TypeScript will not be able to provide type safety, and tools which rely on type data, such as auto completion, will not work. Remember, it should be avoided at "any" cost...

  - unknown - it is a similar, but safer alternative to any.

    - unknown is best used when you don't know the type of data being typed. To add a type later, you'll need to cast it. Casting is when we use the "as" keyword to say property or variable is of the casted type.

  - never - it effectively throws an error whenever it is defined.

    - never is rarely used, especially by itself, its primary use is in advanced generics.

  - undefined & null - undefined and null are types that refer to the JavaScript primitives undefined and null respectively.

```bash
let y: undefined = undefined;
let z: null = null;

```

- TypeScript Arrays

```bash
const names: string[] = [];
names.push("Dylan"); # no error

# The readonly keyword can prevent arrays from being changed.
const names: readonly string[] = ["Dylan"];
names.push("Jack"); # Error: Property 'push' does not exist on type 'readonly string[]'.

# TypeScript can infer the type of an array if it has values.
const numbers = [1, 2, 3]; # inferred to type number[]
const numbers = [1, 2, 3, "a"]; # inferred to type (string | number)[]

numbers.push(4); # no error

```

- TypeScript Tuples
  - A tuple is a typed array with a pre-defined length and types for each index.

```bash
# define our tuple
let ourTuple: [number, boolean, string]; # CONST WILL GIVE ERROR FOR TUPLES [USE LET ONLY]

ourTuple = [5, false, 'Coding']; # initialize correctly
ourTuple = [false, 'Coding God was mistaken', 5]; # wrong order will also gives error
console.log(ourTuple[0]); # To access 1st element

const ourTuple: [string, number] = ["s", 2,2,4];
# YOU CAN WRITE ANY TYPE AFTER THIS
#SO CREATE READONLY TUPLES --NO IT IS GIVING ERROR

# READONLY TUPLES
# define our readonly tuple - YOU CANNOT CHANGE IT LATER
const ourReadonlyTuple: readonly [number, boolean, string] = [5, true, 'Coding'];

# useState in react returns a tuple of the value and a setter function.
#It's a example of tuple : const [firstName, setFirstName] = useState('Dylan')

# NAMED TUPLES ::
# you can access elements by their names, making the code more readable.
const ourTuple: [letter: string, digit: number] = ["s", 2];

# Destructuring Tuples::
# Since tuples are arrays we can also destructure them.
const graph: [number, number] = [55.2, 41.3];
const [x, y] = graph;

```

- TypeScript Object Types

```bash

# OBJECT TYPE

const car: { type: string, model: string, year: number } = {
  type: "Toyota", model: "Corolla", year: 2009 };

# TypeScript can infer the types of properties based on their values.
const ourTuple = { name: "ok" };
ourTuple.name = "go"; # Can change without error
ourTuple.name = 3; # will show error

# Optional Properties::

const car: { type: string, mileage: number } = { # error
  type: "Toyota"
};
const car: { type: string, mileage?: number } = {
# added "?" so mileage property is now optional so no error
  type: "Toyota"
};
car.mileage = 2000;

# Index Signatures::

# this means the key is string and value is number for all the value
const obj: { [index: string]: number } = { one: 1 };
obj.two = 2; # Works fine
obj.three = "three"; # Gives Error

# Index signatures like this one can also be expressed with utility types
# like Record<string, number>.
```

- TypeScript Enums

  - An enum is a special "class" that represents a group of constants (unchangeable variables).
  - Enums come in two flavors string and numeric. Lets start with numeric.

```bash
# Numeric Enums - Default::

# By default, enums will initialize the first value to 0 and add 1 to each additional value:
enum CardinalDirections {
  North,
  East,
  South,
  West,
}
console.log(CardinalDirections.North);  # 0
console.log(CardinalDirections.East);   # 1
console.log(CardinalDirections.["South"]);  # 2 # You can also call it this way
console.log(CardinalDirections.["West"]);   # 3
console.log(CardinalDirections[1]);        # East
console.log(CardinalDirections[3]);        # West
console.log(CardinalDirections[0]);        # North

# Numeric Enums - Initialized::

# If no value is provided then it will add one to next enum value
enum CardinalDirections {
  North = 5,
  East,
  South,
  West,
}
console.log(CardinalDirections.North);  # 5
console.log(CardinalDirections.East);   # 6
console.log(CardinalDirections.South);  # 7
console.log(CardinalDirections.West);   # 8

# Enum can have duplicate values but avoid doing this
enum CardinalDirections {
  North = 5,     # 5
  East,          # 6
  South = 5,     # 5
  West,          # 6
}
# Numeric Enums - Fully Initialized::

enum StatusCodes {
  NotFound = 404,
  Success = 200,
  Accepted = 202,
  BadRequest = 400,
}
console.log(StatusCodes["Accepted"]);    # 404 # You can also write it this way
console.log(StatusCodes["Success"]);     # 200
console.log(StatusCodes.Accepted);       # 202
console.log(StatusCodes.BadRequest);     # 400
console.log(StatusCodes[200]);           # Success

# String Enums ::

# Technically, you can mix and match string and numeric enum values, but it is recommended not to do so.
enum CardinalDirections {
  North = "myNorth",
  East = "myEast",
  South = "mySouth",
  West = "myWest",
}
console.log(CardinalDirections["North"]);     # myNorth
console.log(CardinalDirections["East"]);      # myEast
console.log(CardinalDirections.South);        # mySouth
console.log(CardinalDirections.West);         # myWest
console.log(CardinalDirections["MyWest"]);    # West  #YOU CAN'T CALL BY VALUES (CAN DO IN NUM)

```

- TypeScript "Type" Aliases and "Interfaces"
  - Aliases and Interfaces allows types to be easily shared between different variables/objects.

```bash
1. Type - # allow defining types with a custom name
# Type Aliases can be used for primitives like string or more complex types such as objects and arrays:

# First define the types here
type CarYear = number;
type CarType = string;
type CarModel = string;
type Car = {
  year: CarYear; # Year is number as defined by CarYear
  type: CarType;
  model: CarModel;
};

# Then just use name here
const myCarYear: CarYear = 2001;
const myCarType: CarType = "Toyota";
const myCarModel: CarModel = "Corolla";
const myCar: Car = {
  year: myCarYear,
  type: myCarType,
  model: myCarModel,
};

# Extending types :: - [MEANS ADDING TYPES]
# It means creating a new interface with the same properties as the original, plus something new.
type Name = {
  name: string;
};
type Age = {
  age: number;
};
type Person = Name & Age; # You can add them with "&"
const person: Person = {
  name: "Alice",
  age: 30
};
console.log(person); # { name: "Alice", age: 30 }

2. Interfaces
# Interfaces are similar to type aliases, except they only apply to object types.

interface Rectangle {
  height: number,
  width: number
}

const rectangle: Rectangle = {
  height: 20,
  width: 10
};

# Extending Interfaces ::
# It means creating a new interface with the same properties as the original, plus something new.
interface Rectangle {
  height: number;
  width: number;
}
interface ColoredRectangle extends Rectangle {
  color: string;
  // height: string; # gives error as it contradicts with the extend type {can write same type}
}
const coloredRectangle: ColoredRectangle = {
  height: 20,
  width: 10,
  color: "red"
};

# Declaration Merging :: -> ONLY INTERFACE CAN DO IT AND NOT TYPES
# you can define multiple declarations with the same name, and TypeScript will automatically merge them into a single interface.
interface Person {
  name: string;
}
interface Person {
  age: number;
}
const person: Person = {
  name: "Alice",
  age: 30,
};

*** Differences Between interface and type in TypeScript:
    i- Declaration Merging:
        - Interface: Supports declaration merging.
        - Type: Does not support declaration merging.

    ii- Usage with Classes:
        - Interface: Can be implemented by classes.
        - Type: Can describe class instances but is less idiomatic for class implementation.

    iii- Extending/Intersection:
        - Interface: Uses extends for inheritance.
        - Type: Uses intersection types (&) for combining types.

      4. Function Overloads:
        - Interface: Can define multiple function signatures (overloads).
        - Type: Can define function types but less naturally supports overloads.

      5. Recursive Types:
        - Interface: Naturally suited for recursive structures.
        - Type: Can handle recursive structures but with different syntax.

```

- TypeScript Union Types (Union '|' (OR))
  - Union types are used when a value can be more than a single type.
  - Such as when a property would be string or number.

```bash
# Using the | we are saying our parameter is a string or number
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code}.`);
}
printStatusCode(404);
printStatusCode("404");

# Union Type Errors
# Note: you need to know what your type is when union types are being used to avoid type errors:
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code.toUpperCase()}.`);
}
# The above line will give error as toUpperCase() property is not for numbers::
# YOU CAN SOLVE THIS BY USING "as" (CASTING) FOR PERTICULAR VARIABLE TO SPECIFY THE TYPE
function printStatusCode(code: string | number) {
  console.log(`My status code is ${(code as string).toUpperCase()}.`);
}


```

- TypeScript Functions

```bash

1. Return Type

# What type of value this function will return - MOST OF THE TIME IT WILL INFER
function getTime(): number { # REMOVING RETURN TYPE THE FUNCTION WILL INFER THE TYPE HERE
  return new Date().getTime();
}
# If no return type is defined, TypeScript will attempt to infer it through the types of the variables or expressions returned.

# Void Return Type ::
function printHello(): void {
  console.log('Hello!');
}

2. Parameters

# Function parameters are typed with a similar syntax as variable declarations.
function multiply(a: number, b: number) {
  return a * b;
}

# Optional Parameters :: "?"

# By default TypeScript will assume all parameters are required, but they can be explicitly marked as optional.
// the `?` operator here marks parameter `c` as optional
function add(a: number, b: number, c?: number) {
  return a + b + (c || 0);
}

# Default Parameters :: "="

# The default value goes after the type annotation:
function pow(value: number, exponent: number = 10) {
  return value ** exponent;
}

# Named Parameters :: "{}:{}"

function divide({ dividend, divisor }: { dividend: number, divisor: number }) {
  return dividend / divisor;
}

# YOU CAN CREATE TYPE FOR NAMED PARAMETERS THIS WAY
type Finding2 = (p: { x: string; y: number }) => number;

# Rest Parameters :: "..."

# Rest parameters can be typed like normal parameters, but the type must be an array as rest parameters are always arrays.
function add(a: number, b: number, ...rest: number[]) {
  return a + b + rest.reduce((p, c) => p + c, 0);
}

3. Type Alias for functions

# Function types can be specified separately from functions with type aliases.
# These types are written similarly to arrow functions
# ONLY USED FOR FUNCTION EXPRESSION(VARIABLE FN) AND NOT FUNCITON DECLARATION(NORMAL FN)
# FOR FUNCTION DECLARATION USE INLINE TYPES OR MAY USE UTILITY TYPES (BUT AVOID THIS)

type FuncitonType = (age: number) => String;

const addAge: FuncitonType = (age) => {
  // return 3; # This will give error as return type is specified to string and not number
  return `Your age is ${age}`;
};

```

- TypeScript Casting
  - Casting is the process of overriding a type.

```bash

1. Casting with as

let x: unknown = "hello";
console.log((x as string).length);

# Casting doesn't actually change the type of the data within the variable
let x: unknown = 1;
console.log((x as string).length); # returns undefined (as won't change 1 into "1")
// console.log((2 as string).length); # This will give error as it's a number directly

# Force casting
# To override type errors that TypeScript may throw when casting, first cast to unknown, then to the target type.
console.log((2 as unknown as string).length); # convert number to unknown first (if intentional)-> STILL GIVE ERROR (JAVASCRIPT) CANNOT USE LENGTH AS IN NUMBER

2. Casting with <>

const x: number | string = "3";
# below both are same
console.log((x as string).toUpperCase());
console.log((<string>x).toUpperCase());

#  Here x is number so type conversion will give error (to solve this first convert them into unknown)
const x: number | string = 3;
// console.log((x as string).toUpperCase()); # Error TYPESCRIPT
// console.log((<string>x).toUpperCase()); # Error TYPESCRIPT
console.log((x as unknown as string).toUpperCase()); # Error JAVASCRIPT ( NO TYPESCRIPT)
console.log((<string>(<unknown>x)).toUpperCase()); # Error JAVASCRIPT ( NO TYPESCRIPT)

```

- TypeScript Classes
  - TypeScript adds types and visibility modifiers to JavaScript classes.

```bash
1. Members: Types

# The members of a class (properties & methods) are typed using type annotations, similar to variables.
class Person {
  name: string;
}
const person = new Person();
person.name = "Jane";

2. Members: Visibility

# There are three main visibility modifiers in TypeScript.
    #1. public - (default) allows access to the class member from anywhere
    #2. private - only allows access to the class member from within the class
    #3. protected - allows access to the class member from itself and any classes that inherit it

class Testing {
  public name: string; # You need to write this to write it in construction
  private age: number; # this can't be access outsite this class
  public constructor(name: string, age: number) { # NO NEED TO WRITE PUBLIC AS IT'S DEFAULT
    this.name = name;
    this.age = age;
  }
  public get getInfo1() { # NO NEED TO WRITE PUBLIC AS IT'S DEFAULT
    return `My name is ${this.name}, and my age is ${this.age}`;
  }
  public getInfo2() {
    return `My name is ${this.name}, and my age is ${this.age}`;
  }
  private getInfo3() {
    return `My name is ${this.name}, and my age is ${this.age}`;
  }
}
const myName = new Testing("Mahesh", 28);
// console.log(myName.age);  # age is private so can't be call here
console.log(myName.name);
console.log(myName.getInfo1);
console.log(myName.getInfo2());
// console.log(myName.getInfo3()); # getInfo3 is private so can't be called here


# Parameter Properties
# TypeScript provides a convenient way to define class members in the constructor, by adding a visibility modifiers to the parameter.

# This line declares and initialize the properties -> This line is same as below 5 lines
public constructor(private name: string, public age: number) {}

# NO NEED TO WRITE THIS 5 LINES NOW
    # public name: string;
    # private age: number;
    # public constructor(name: string, age: number) {
    # this.name = name;
    # this.age = age;

3. Readonly
# readonly keyword can prevent class members from being changed.

class Person {
  private readonly name: string; # This is readonly

  public constructor(name: string) {
    # name cannot be changed after this initial definition, which has to be either at it's declaration or in the constructor.
    this.name = name;
  }
  public getName(): string {
    return this.name;
  }
  set changeName(newName: string) {
    // this.name = newName; # This will give error as name property is readonly
  }
}
const person = new Person("Jane");
console.log(person.getName());

4. Inheritance: Implements
# Interfaces can be used to define the type a class must follow through the implements keyword.

interface GetNameType {
  getName: () => string; # the getName method will return string. It will be in GetNameType
  greet: () => string;
}
type NewGreet = { # You can use type or interface here
  morningGreet: () => string;
}

# Use implements to add interface and use ,(comma) to add multiple interface
class Naming implements GetNameType, NewGreet {
  constructor(protected readonly name: string) {} # Use protected as it needed in different class
  getName(): string { # Can skip string as it gets infer
    return this.name;
  }
  greet() {
    return `Hello!, ${this.name}`;
  }
  morningGreet() {
    return `Morning, ${this.name}`;
  }
}
const myName = new Naming("Mahesh");

console.log(myName.getName());      # Mahesh
console.log(myName.greet());        # Hello!, Mahesh
console.log(myName.morningGreet()); # Morning, Mahesh

5. Inheritance: Extends
# Classes can extend each other through the extends keyword.
# A class can only extends ONE OTHER CLASS.
6. Override
# When a class extends another class, it can replace the members of the parent class with the same name.
# The override function is default (means you can change the parent function without writing the override keyword). To force it to be used when overriding, Use the setting noImplicitOverride in tsconfig(maybe)

# You can avoid such types as TS can infer it
interface GetSquare {
  fullInfo: () => string;
}

class Square extends Naming implements GetSquare {
  constructor(private readonly length: number, name: string) {
    super(name); # To add property from extended class use super
  }
  # The getName() function has override the function(with same name) from extended Naming class
  override getName(): string {
    return ` Overriding the getName() function from Naming class`;
  }

  morningGreet() {
    return `Morning, ${this.name}`;
  }
  get squareValue() {
    return this.length * this.length;
  }
  fullInfo() {
    return `total length is ${this.squareValue}`;
  }
}

const myName = new Square(12, "Mahesh");
console.log(myName.getName());
console.log(myName.morningGreet());
console.log(myName.squareValue);
console.log(myName.fullInfo());

7. Abstract Classes
# Classes can be written in a way that allows them to be used as a base class for other classes without having to implement all the members. This is done by using the abstract keyword. Members that are left unimplemented also use the abstract keyword.

# NOT DOING IT NOW..

```

###TypeScript Basic Generics

- Generics in TypeScript allow you to create reusable components that work with a variety of types rather than a single type.

- They provide a way to create functions, classes, and interfaces that can operate with different data types while maintaining type safety.

- They enable you to write flexible and reusable code.

- Generics: Allow for type-safe and reusable code components.
- Generic Functions: Define functions that work with any type.
- Generic Classes: Create classes that operate with various types.
- Generic Interfaces and types: Describe objects with properties of different types.
- Generic Constraints: Restrict generics to types with specific properties.

```bash

1. Generic Functions # Define functions that work with any type.

function createPair<S, T>(v1: S, v2: T): [S, T] {
  return [v1, v2];
}
console.log(createPair<string, number>("hello", 42));
console.log(createPair<number, number>(2, 42));
console.log(createPair<string, boolean>("Are you good", false));
console.log(createPair("ok", 2)); # WORKS FINE, Type can be infer by typescript
console.log(createPair("ok", 2, 3)); # Will give error as only 2 parameters are allowed
console.log(createPair("ok")); # Will give error as only 2 parameters are allowed

2. Generic Classes # Create classes that operate with various types.

class NamedValue<T> {
  private _value: T | undefined;

  constructor(private name: string) {}

  public setValue(value: T) {
    this._value = value;
  }
  public getValue(): T | undefined {
    return this._value;
  }
  public toString(): string {
    return `${this.name}: ${this._value}`;
  }
}

let value = new NamedValue<number>("myNumber");
let value2 = new NamedValue<string>("myNumber");
value.setValue(10);
value2.setValue("OK");
console.log(value.toString()); // myNumber: 10
console.log(value2.toString()); // myNumber: OK

3. Generic Interfaces and types # Describe objects with properties of different types.

type ObjType<T, U> = { name: T; age: U };
interface NewObjType<S, T> {
  firstName: S;
  lastName: S;
  age: T;
}

const obj: ObjType<string, number> = { name: "Mahesh", age: 3 };
const newObj: NewObjType<string, number> = {
  firstName: "Mahesh",
  lastName: "Kumar",
  age: 28,
};

# Default Value ::

# Generics can be assigned default types which apply if no other value is "specified" or "inferred".

type ObjType<T = string, U = number> = { name: T; age: U };
const obj: ObjType = { name: "Mahesh", age: 3 };
const obj: ObjType<string, string> = { name: "Mahesh", age: "three" }; # you can change the default

4. Generic Constraints(Extends)
# Constraints can be added to generics to limit what's allowed.
# The constraints make it possible to rely on a more specific type when using the generic type.

# example 1
function createLoggedPair<S extends string | number, T extends string | number>(
  v1: S,
  v2: T
): [S, T] {
  console.log(`creating pair: v1='${v1}', v2='${v2}'`);
  return [v1, v2];
}
createLoggedPair("Hello", "Fine");
createLoggedPair("Hello", 101);
// createLoggedPair("Hello", true); # Error as boolean doesn't exists on type

#Example 2
# Constrain T to types that have a length property (IF HAVE x.length property)
function logLength<T extends { length: number }>(arg: T): void {
  console.log(arg.length);
}
logLength("Hello");        # Works, string has a length property
logLength([1, 2, 3]);      # Works, array has a length property
// logLength(42);          # Error: number doesn't have a length property

# CAN ADD INTERFACE/TYPES FOR IT
interface Lengthwise {
  length: number;
}
function logLength<T extends Lengthwise>(arg: T): void {
  console.log(arg.length);
}
logLength("Hello");
```

- TypeScript Utility Types
  - TypeScript comes with a large number of types that can help with some common type manipulation, usually referred to as utility types.
  - [Partial, Required, Record, Omit, Pick, Exclude, ReturnType, Parameters, ReadOnly]

```bash
1. Partial # It changes all the properties in an object to be optional.

interface NewId {
  one: number;
  two: number;
}
const obj1: NewId = { one: 2, two: 4 };
const obj2: Partial<NewId> = { one: 2 }; # Now all obj are optional

2. Required # It changes all the properties in an object to be required.

interface NewId {
  one?: number;
  two?: number;
}
const obj1: NewId = { one: 2 };
const obj2: Required<NewId> = { one: 2, two: 4 }; # All are required/compulsory

3. Record # It is a shortcut to defining an object type with a specific key type and value type.
# Record<string, number> is equivalent to { [key: string]: number } (tuples)
const nameAgeMap: Record<string, number> = {
  'Alice': 21,
  'Bob': 25
};

4. Omit # It removes keys from an object type. -> [only for object type]

interface Person {
  name: string;
  age: number;
  location?: string;
}
# age and location are removed from the type
const bob: Omit<Person, "age" | "location"> = { name: "Bob" };

5. Pick # It removes all but the specified keys from an object type.

interface Person {
  name: string;
  age: number;
  location?: string;
}
# Except age all other properties are removed
const bob: Pick<Person, "age"> = { age: 23 };

6. Exclude # It removes types from a union.

type Primitive = string | number | boolean;
const value1: Exclude<Primitive, string> = true;
const value2: Exclude<Primitive, string> = 234;
// const value3: Exclude<Primitive, string> = "abc"; # It will give error as string has been excluded from the union type

7. ReturnType # It extracts the return type of a function type.

type PointGenerator = () => { x: number; y: number };
# It will give type of what a function will return
const point: ReturnType<PointGenerator> = {
  x: 10,
  y: 20,
};
console.log(point);

8. Parameters # It extracts the parameter types of a function type as an array.

type Finding = (x: string, y: number) => number;
type Finding2 = (p: { x: string; y: number }) => number;

const value1: Parameters<Finding> = ["name", 8];
const value2: Parameters<Finding2> = [{ x: "name", y: 8 }];

# How both are different in writing a function
const find: Finding = (x, y) => {
  return y + x.length;
};
const find2: Finding2 = (p) => {
  return p.y + p.x.length;
};
const find3: Finding2 = ({ x, y }) => {
  return y + x.length;
};

console.log(find("hello", 5)); // Output: 10
console.log(find2({ x: "hello", y: 5 })); // Output: 10
console.log(find3({ x: "hello", y: 5 })); // Output: 10

9. Readonly
# It is used to create a new type where all properties are readonly, meaning they
# cannot be modified once assigned a value.
# Keep in mind TypeScript will prevent this at compile time, but in theory since
# it is compiled down to JavaScript you can still override a readonly property.
interface Person {
  name: string;
  age: number;
}
const person: Readonly<Person> = {
  name: "Dylan",
  age: 35,
};
// person.name = "Israel"; # This will give error as it's readonly

```

- TypeScript Keyof
  - It is a keyword in TypeScript which is used to extract the key type from an object type.

```bash
1. keyof with explicit keys
# It is used to create a union type of the keys of a given object type.

# Example 1
interface Person {
  name: string;
  age: number;
  location: string;
}
type PersonKeys = keyof Person; # 'name' | 'age' | 'location'

const myPerson: PersonKeys = "age"; # You can only write any one value from the three

# Example 2
interface Person {
  name: string;
  age: number;
}
# `keyof Person` means "name" | "age"
function printPersonProperty(person: Person, property: keyof Person) {
  console.log(`Printing person property ${property}: "${person[property]}"`);
}
let person = {
  name: "Max",
  age: 27,
};
printPersonProperty(person, "name"); # Can only write "name" or "age" here

2. keyof with index signatures ->[NOT IMP MAY BE]
# keyof can also be used with index signatures to extract the index type.

type StringMap = { [key: string]: unknown };
# `keyof StringMap` resolves to `string` here
function createStringPair(property: keyof StringMap, value: string): StringMap {
  return { [property]: value };
}
console.log(createStringPair(22, "OOOOKKK")); // { '22': 'OOOOKKK' }
console.log(createStringPair("abc", "OOOOKKK")); // { '22': 'OOOOKKK' }
// console.log(createStringPair(true, "OOOOKKK")); // Error

# key must be 'string', 'number', 'symbol' and that too gets converted into string(?)
# In JavaScript, when you use a number as an object key, it is internally
# converted to a string. This behavior causes TypeScript to include
# both string and number in the keyof type.
```

- TypeScript Null & Undefined
  - By default null and undefined handling is disabled, and can be enabled by setting strictNullChecks to true.

```bash
# null and undefined are primitive types and can be used like other types, such as string.
let value: string | undefined | null = null;
value = 'hello';
value = undefined;

```
