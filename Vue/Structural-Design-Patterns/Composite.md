# Composite

In Vue.js version 3 with script setup, the Composite Design Pattern can be used to treat individual components and groups of components in a uniform way. It allows you to compose nested structures of components and treat them as a single component. This pattern is useful when you want to represent part-whole hierarchies of components.

Let's create an example of using the Composite Design Pattern to implement a composite component in a component library. We'll have a `Box` component that can contain other `Box` components as its children, creating a nested structure.

1. Create the Composite Component:

```vue
<!-- Box.vue -->
<template>
  <div :style="boxStyle">
    <slot></slot>
  </div>
</template>

<script setup>
const boxStyle = { padding: '10px', border: '1px solid black' };
</script>
```

2. Use the Composite Component:

```vue
<!-- MyComponent.vue -->
<template>
  <Box>
    <Box>
      <Box>
        <p>This is a nested Box component</p>
      </Box>
      <p>This is a child paragraph</p>
    </Box>
    <Box>
      <p>This is another child paragraph</p>
    </Box>
  </Box>
</template>

<script setup>
import Box from './Box.vue';
</script>
```

In this example, we have created a `Box` component that acts as the composite component. It simply renders a `<div>` element with a border and padding to visually represent the box. It also has a `<slot>` element to allow other components to be placed inside it.

In the `MyComponent.vue`, we are using the `Box` component to create a nested structure. The outermost `Box` contains two child `Box` components, each of which may contain more child `Box` components or other elements like `<p>`.

By using the Composite Design Pattern, we can treat each `Box` component and its children as a single entity. This allows us to create complex component structures while keeping the code simple and easy to maintain. Additionally, it enables us to build reusable component structures that can be easily composed to form larger layouts in the component library.