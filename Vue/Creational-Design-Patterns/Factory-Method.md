# Factory Method

The Factory Method Design Pattern in Vue.js version 3 allows you to create objects (components) without specifying the exact class (component) that will be instantiated. It provides an interface for creating objects, but the subclasses (concrete components) can decide which class to instantiate. This pattern promotes loose coupling and enhances flexibility in component creation. Let's see how you can implement the Factory Method Pattern in a Vue.js version 3 component library:

Example: Creating a factory for generating different types of buttons.

```vue
<!-- ButtonFactory.js -->
<template>
  <button :class="buttonClass" @click="onClick">
    {{ label }}
  </button>
</template>

<script setup>
import { ref } from 'vue';

const props = {
  label: String,
  onClick: Function,
  variant: {
    type: String,
    default: 'default',
  },
};

const buttonClass = ref('');

// Set the button class based on the variant prop
if (props.variant === 'primary') {
  buttonClass.value = 'btn-primary';
} else if (props.variant === 'secondary') {
  buttonClass.value = 'btn-secondary';
} else {
  buttonClass.value = 'btn-default';
}
</script>
```

Usage:

```vue
<!-- App.vue -->
<template>
  <div>
    <ButtonFactory :label="'Default Button'" />
    <ButtonFactory :label="'Primary Button'" :variant="'primary'" />
    <ButtonFactory :label="'Secondary Button'" :variant="'secondary'" />
  </div>
</template>

<script setup>
import ButtonFactory from './components/ButtonFactory';
</script>
```

In this example, the `ButtonFactory` component serves as the factory that creates different types of buttons based on the `variant` prop. The `App.vue` file uses the `ButtonFactory` to create different buttons with different variants.

By using the Factory Method Pattern, you can easily extend your component library and create new components without modifying the existing ones. It promotes flexibility and reusability, making it easier to manage and maintain your Vue.js component library.