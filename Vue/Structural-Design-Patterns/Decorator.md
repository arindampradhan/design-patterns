# Decorator

In Vue.js version 3 with script setup, the Decorator Design Pattern can be used to add additional functionality or behavior to components dynamically. It allows you to extend the behavior of a component without modifying its original code. This pattern is useful when you want to add features to components at runtime or when you need to add behavior to multiple components in a flexible way.

Let's create an example of using the Decorator Design Pattern to implement a decorator component that adds a custom style to another component.

1. Create the Decorator Component:

```vue
<!-- Decorator.vue -->
<template>
  <div :style="decoratedStyle">
    <slot></slot>
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';

const decoratedStyle = ref({ border: '2px solid red', padding: '10px' });
provide('decoratedStyle', decoratedStyle);
</script>
```

2. Use the Decorator Component:

```vue
<!-- MyComponent.vue -->
<template>
  <Decorator>
    <h2>This is the decorated title</h2>
  </Decorator>
</template>

<script setup>
import Decorator from './Decorator.vue';
import { inject } from 'vue';

const decoratedStyle = inject('decoratedStyle');
</script>
```

In this example, we have created a `Decorator` component that acts as the decorator. It renders a `<div>` element with a custom style (a red border and padding) and provides this style to its children using the `provide` function from Vue. The `decoratedStyle` ref is used to store the style, and it is passed down to its children using the `provide` function.

In the `MyComponent.vue`, we are using the `Decorator` component to decorate the `<h2>` element. The `MyComponent` simply contains the `Decorator` component, and inside it, we have the `<h2>` element that will be styled by the decorator.

By using the Decorator Design Pattern, we can add custom styles or behaviors to components dynamically without modifying their original code. This makes the code more flexible and maintainable, as we can easily add or remove decorators as needed. Additionally, it allows us to create reusable decorators that can be applied to multiple components in the component library.