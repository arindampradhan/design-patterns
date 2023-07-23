# Prototype

In Vue.js version 3 with script setup, you can implement the Prototype Design Pattern using the `ref` function to create a reactive reference to the prototype object. Here's an example of how to do it:

```vue
<template>
  <div>
    <h1>Prototype Component</h1>
    <p>Instance ID: {{ instanceId }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Define the prototype object
const prototypeObject = {
  instanceId: Date.now(), // Generate a unique ID for the instance
};

// Create a reactive reference to the prototype object
let instance = ref({ ...prototypeObject });

// Function to create a new instance based on the prototype
function createInstance() {
  instance.value = { ...prototypeObject };
}
</script>
```

In this example, we first define the `prototypeObject` which contains the shared properties and methods that will serve as the prototype for all instances of the component.

Then, we use the `ref` function to create a reactive reference named `instance` and initialize it with a copy of the `prototypeObject`. This ensures that all instances start with the same initial state from the prototype.

Next, we define a function called `createInstance`, which creates a new instance based on the prototype. It does this by copying the properties and methods from the `prototypeObject` to the `instance.value`.

Now, whenever you use this component in different parts of the application and create new instances, each instance will start with the same initial state from the prototype. Any modifications made to one instance will not affect the others, as they all have their separate reactive references.

Usage of the PrototypeComponent in other parts of the application:

```vue
<template>
  <div>
    <PrototypeComponent />
  </div>
</template>

<script setup>
import PrototypeComponent from './PrototypeComponent.vue';
</script>
```

When `PrototypeComponent` is used in different parts of the application and multiple instances are created, each instance will have its unique `instanceId` generated at the time of creation, but they will share the same initial state from the prototype.