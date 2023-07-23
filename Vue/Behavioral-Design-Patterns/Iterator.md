# Iterator

The Iterator Design Pattern is a behavioral design pattern that provides a way to access elements of a collection without exposing its underlying representation. In the context of a Vue.js component library with script setup, the Iterator Pattern can be used to abstract the iteration process for collections within components, allowing consumers to traverse the elements without knowing the internal structure.

To implement the Iterator Design Pattern in a Vue.js component library using Vue.js version 3 with script setup, we can create an iterator that works with arrays as the collection.

Let's create a simple example of a component that uses the Iterator Pattern to iterate over an array of items and display them:

```vue
<template>
  <div>
    <ul>
      <li v-for="item in itemsIterator" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

// Sample array of items
const items = ref([
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
  { id: 3, name: 'Item 3' },
]);

// Create a computed property for the itemsIterator
const itemsIterator = computed(() => createIterator(items.value));

// Function to create an iterator for the array
function createIterator(collection) {
  let index = 0;

  return {
    next() {
      if (index < collection.length) {
        return { value: collection[index++], done: false };
      } else {
        return { done: true };
      }
    },
  };
}
</script>
```

In this example, we have a component that renders an array of items using `v-for`. The `itemsIterator` is a computed property that uses the `createIterator` function to create an iterator for the `items` array.

The `createIterator` function returns an object with a `next` method that, when called, retrieves the next item from the collection and advances the iterator. The `done` property is used to indicate if there are no more items to iterate.

When the component is used in an application, it will automatically iterate over the `items` array without exposing the array itself to the consuming code.

You can then use the component in another app like this:

```vue
<template>
  <div>
    <MyListComponent />
  </div>
</template>

<script setup>
import MyListComponent from 'path-to-your-component-library';
</script>
```

By using the Iterator Pattern, you provide a clean and encapsulated way for consumers to access the elements of a collection in your Vue.js component library. This abstraction allows you to modify the internal representation of the collection without affecting the consuming code.