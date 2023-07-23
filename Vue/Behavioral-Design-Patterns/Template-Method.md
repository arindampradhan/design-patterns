# Template Method

The Template Method Design Pattern is a behavioral design pattern that defines the skeleton of an algorithm in a method but allows subclasses to override some steps of the algorithm without changing its structure. In the context of a Vue.js component library with script setup, the Template Method Pattern can be used to provide a blueprint for the component's rendering process while allowing consumers to customize certain parts of the rendering.

To implement the Template Method Design Pattern in a Vue.js component library using Vue.js version 3 with script setup, we can use component composition and scoped slots to define the template method and allow consumers to customize the rendering of specific parts.

Let's create an example of a simple component that uses the Template Method Pattern to render a generic list:

```vue
<template>
  <div>
    <ul>
      <li v-for="item in items" :key="item.id">
        <!-- Use scoped slot to customize the rendering of each item -->
        <slot :item="item">{{ item.name }}</slot>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const items = ref([
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
  { id: 3, name: 'Item 3' },
]);
</script>
```

In this example, we have a component that renders a list of items (`<li>`) using `v-for`. Instead of directly rendering the item name, we use a scoped slot to allow consumers to customize the rendering of each item.

Now, let's use the component in another app:

```vue
<template>
  <div>
    <MyList>
      <!-- Custom rendering for each item using scoped slot -->
      <template v-slot="{ item }">
        <span>{{ item.name }} (ID: {{ item.id }})</span>
      </template>
    </MyList>
  </div>
</template>

<script setup>
import MyList from 'path-to-your-component-library';
</script>
```

In this example, we use the `MyList` component from the component library and provide a scoped slot with custom rendering for each item. The scoped slot receives the `item` object, and we use it to display the item's name and ID.

By using the Template Method Pattern with scoped slots in Vue.js, you allow consumers of your component library to customize the rendering of specific parts of the component without having to modify the component's source code. This promotes reusability and flexibility in your component library, enabling users to tailor the component to their specific needs.