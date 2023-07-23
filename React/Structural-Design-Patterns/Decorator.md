# Decorator

The Decorator Design Pattern is a structural design pattern that allows behavior to be added to individual objects dynamically without affecting the behavior of other objects from the same class. In the context of a React component library, you can use the Decorator Pattern to enhance or extend the functionality of your components without modifying their source code directly.

To implement the Decorator Design Pattern in a React component library, you can use higher-order components (HOCs) or render props to add additional functionality to your components.

Let's see how you can implement the Decorator Design Pattern using HOCs in a React component library:

1. Set up the Component Library
Start by creating a new React component library project or use an existing one.

2. Create the Decorator Components
Create one or more decorator components that enhance the functionality of your existing components. Each decorator component should be a higher-order component (HOC) that takes a component as input and returns a new component with additional functionality.

```jsx
// withBorder.js
import React from 'react';

const withBorder = (WrappedComponent) => {
  return (props) => (
    <div style={{ border: '2px solid black' }}>
      <WrappedComponent {...props} />
    </div>
  );
};

export default withBorder;
```

```jsx
// withBackground.js
import React from 'react';

const withBackground = (WrappedComponent) => {
  return (props) => (
    <div style={{ background: 'lightgray' }}>
      <WrappedComponent {...props} />
    </div>
  );
};

export default withBackground;
```

3. Use the Decorator Components in Your App Component
Now, you can use the decorator components to enhance the functionality of your existing components.

```jsx
import React from 'react';
import withBorder from 'path-to-your-component-library/withBorder';
import withBackground from 'path-to-your-component-library/withBackground';

const MyComponent = ({ text }) => {
  return <div>{text}</div>;
};

const MyComponentWithBorder = withBorder(MyComponent);
const MyComponentWithBackground = withBackground(MyComponent);

const App = () => {
  return (
    <div>
      <h2>Component with Border</h2>
      <MyComponentWithBorder text="Hello, with Border!" />

      <h2>Component with Background</h2>
      <MyComponentWithBackground text="Hello, with Background!" />
    </div>
  );
};

export default App;
```

In this example, we have two decorator components, `withBorder` and `withBackground`, which add a border and a background to the wrapped component, respectively. We use these decorator components to enhance the functionality of our `MyComponent` component.

By using the Decorator Design Pattern with higher-order components (HOCs), you can dynamically add behavior or functionality to your existing components without modifying their source code. This approach promotes reusability and composability within your component library, allowing consumers to customize the behavior of the components easily.