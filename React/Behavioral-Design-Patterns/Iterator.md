# Iterator

In a React component library, you can implement the Iterator Design Pattern to provide a way to access elements of a collection (such as an array) without exposing the underlying representation of the collection. The Iterator Pattern can be useful for creating components that iterate over data and allow consumers to traverse the data without knowing the internal structure.

Let's see how you can implement the Iterator Design Pattern in a React component library:

1. Set up the Component Library
Start by creating a new React component library project or use an existing one.

2. Create the Iterator Component
Create an iterator component that accepts an array of data as props and renders each item using a render function (or a child function).

```jsx
// Iterator.js
import React from 'react';

const Iterator = ({ data, renderItem }) => {
  return <div>{data.map((item) => renderItem(item))}</div>;
};

export default Iterator;
```

3. Use the Iterator Component in a List Component
Now, you can use the `Iterator` component within your list component to render a list of items.

```jsx
// List.js
import React from 'react';
import Iterator from './Iterator';

const List = ({ items }) => {
  const renderItem = (item) => {
    return <div key={item.id}>{item.name}</div>;
  };

  return <Iterator data={items} renderItem={renderItem} />;
};

export default List;
```

In this example, we create a `List` component that uses the `Iterator` component to render a list of items. The `renderItem` function is passed to the `Iterator` as a prop and is responsible for rendering each item in the list.

4. Use the Component Library in Another App
Now, you can publish your component library or use it in another React app. To use the `List` component, consumers can pass an array of data to be rendered:

```jsx
import React from 'react';
import List from 'path-to-your-component-library/List';

const App = () => {
  const items = [
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' },
  ];

  return (
    <div>
      <List items={items} />
    </div>
  );
};

export default App;
```

In this example, we use the `List` component from the component library and pass an array of `items` to be rendered.

By implementing the Iterator Design Pattern in your React component library, you provide a clean and encapsulated way for consumers to access and iterate over data without directly dealing with the internal structure of the collection. This promotes reusability and separation of concerns within your component library.