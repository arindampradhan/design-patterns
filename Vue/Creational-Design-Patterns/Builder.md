# Builder

In Vue.js version 3 with script setup, you can implement the Builder Design Pattern to construct complex objects step by step using a builder class. Here's an example of how to do it:

Let's say we want to build a `Person` object with various properties such as name, age, gender, and occupation using a builder pattern.

1. Create the `Person` class:

```vue
<!-- Person.vue -->
<template>
  <div>
    <h1>Person Information</h1>
    <p>Name: {{ person.name }}</p>
    <p>Age: {{ person.age }}</p>
    <p>Gender: {{ person.gender }}</p>
    <p>Occupation: {{ person.occupation }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Define the Person class
class Person {
  constructor() {
    this.name = '';
    this.age = 0;
    this.gender = '';
    this.occupation = '';
  }
}
const person = ref(new Person());
</script>
```

2. Create the `PersonBuilder` class to construct the `Person` object step by step:

```vue
<!-- PersonBuilder.vue -->
<script setup>
import { ref } from 'vue';

// Define the PersonBuilder class
class PersonBuilder {
  constructor() {
    this.person = new Person();
  }

  setName(name) {
    this.person.name = name;
    return this;
  }

  setAge(age) {
    this.person.age = age;
    return this;
  }

  setGender(gender) {
    this.person.gender = gender;
    return this;
  }

  setOccupation(occupation) {
    this.person.occupation = occupation;
    return this;
  }

  build() {
    return this.person;
  }
}

const personBuilder = ref(new PersonBuilder());
</script>
```

3. Now you can use the `PersonBuilder` to construct the `Person` object step by step:

```vue
<!-- App.vue -->
<template>
  <div>
    <h1>Builder Design Pattern Example</h1>
    <button @click="buildPerson">Build Person</button>
    <Person :person="createdPerson" v-if="createdPerson" />
  </div>
</template>

<script setup>
import Person from './Person.vue';
import { ref } from 'vue';

const createdPerson = ref(null);

function buildPerson() {
  createdPerson.value = personBuilder.value
    .setName('John Doe')
    .setAge(30)
    .setGender('Male')
    .setOccupation('Engineer')
    .build();
}
</script>
```

In this example, we have created the `Person` class with its properties (name, age, gender, occupation) and the `PersonBuilder` class to construct a `Person` object step by step. The `PersonBuilder` class has methods (`setName`, `setAge`, `setGender`, `setOccupation`) to set the properties of the `Person` object, and the `build` method to return the final constructed `Person` object.

In the `App.vue`, when the "Build Person" button is clicked, it calls the `buildPerson` function, which uses the `PersonBuilder` to create a new `Person` object with the specified properties. The constructed `Person` object is then displayed using the `Person` component.