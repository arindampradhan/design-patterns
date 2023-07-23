# Strategy

The Strategy Design Pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each one, and makes them interchangeable. The pattern allows the client to choose the algorithm to use at runtime without modifying the client's code. In the context of a Vue.js component library with script setup, the Strategy Pattern can be used to provide different strategies or behaviors for a component, allowing consumers to customize the component's functionality without modifying its source code.

To implement the Strategy Design Pattern in a Vue.js component library using Vue.js version 3 with script setup, we can use function injection to allow consumers to provide custom strategies to the component.

Let's create an example of a component that uses the Strategy Pattern to apply different formatting strategies to a text:

```vue
<template>
  <div>
    <p>{{ formatText(text) }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const text = ref('');

// Function to format the text using the strategy
const formatText = (text) => {
  // Use the strategy function provided by the consumer
  return formatStrategy.value(text);
};

// Default strategy: no formatting
const defaultFormatStrategy = (text) => {
  return text;
};

// Create a ref to hold the strategy function
const formatStrategy = ref(defaultFormatStrategy);

// Function to set the strategy
const setFormatStrategy = (strategy) => {
  formatStrategy.value = strategy;
};
</script>
```

In this example, we have a component that renders a paragraph (`<p>`) with the text provided. The `formatText` function takes the input text and applies the strategy function provided by the consumer to format the text.

The `defaultFormatStrategy` is the default behavior that doesn't apply any formatting. We use the `formatStrategy` ref to store the current strategy, which defaults to the `defaultFormatStrategy`.

The `setFormatStrategy` function allows consumers to change the formatting strategy dynamically. They can pass their custom formatting function, and the component will use that function to format the text.

Now let's use the component in another app:

```vue
<template>
  <div>
    <MyFormattedText :text="message" />
    <button @click="toggleFormat">Toggle Format</button>
  </div>
</template>

<script setup>
import MyFormattedText, { setFormatStrategy } from 'path-to-your-component-library';
import { ref } from 'vue';

const message = ref('Hello, world!');
const isFormatted = ref(true);

// Custom format strategy
const customFormatStrategy = (text) => {
  return text.toUpperCase();
};

// Set the custom format strategy on component mount
onMounted(() => {
  setFormatStrategy(customFormatStrategy);
});

// Toggle format strategy on button click
const toggleFormat = () => {
  if (isFormatted.value) {
    setFormatStrategy(defaultFormatStrategy);
  } else {
    setFormatStrategy(customFormatStrategy);
  }
  isFormatted.value = !isFormatted.value;
};
</script>
```

In this example, we import the `MyFormattedText` component and the `setFormatStrategy` function from the component library. We also define a custom format strategy `customFormatStrategy`, which converts the text to uppercase.

On component mount, we use `setFormatStrategy` to set the custom format strategy for `MyFormattedText`. When the "Toggle Format" button is clicked, we switch between the custom and default format strategies, effectively changing the formatting behavior of the component at runtime.

By using the Strategy Pattern, you enable consumers of your Vue.js component library to easily customize the behavior of components without the need to modify the component's source code. This promotes code reusability and flexibility in your component library.