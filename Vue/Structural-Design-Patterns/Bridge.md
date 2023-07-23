# Bridge

In Vue.js version 3 with script setup, the Bridge Design Pattern can be used to decouple an abstraction from its implementation, allowing them to vary independently. This pattern is useful when you have multiple implementations for a feature or functionality, and you want to switch between them without changing the client code.

Let's create an example of using the Bridge Design Pattern to implement a notification system in a component library. We'll have two different notification types: `AlertNotification` and `ToastNotification`. The Bridge Design Pattern will allow us to switch between these notification types without modifying the client code (the component that uses the notifications).

1. Create the Abstraction and Implementations:

```js
<!-- Notification.js (Abstraction) -->
class Notification {
  constructor(implementation) {
    this.implementation = implementation;
  }

  show(message) {
    this.implementation.show(message);
  }
}

<!-- AlertNotification.js (Concrete Implementation) -->
class AlertNotification {
  show(message) {
    alert(`ALERT: ${message}`);
  }
}

<!-- ToastNotification.js (Concrete Implementation) -->
class ToastNotification {
  show(message) {
    // Implement the logic to show a toast notification here
    console.log(`TOAST: ${message}`);
  }
}
```

2. Use the Bridge in the component:

```vue
<!-- MyComponent.vue -->
<template>
  <div>
    <button @click="showNotification">Show Notification</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Notification from './Notification.js';
import AlertNotification from './AlertNotification.js'; // Concrete Implementation
import ToastNotification from './ToastNotification.js'; // Concrete Implementation

const notificationType = ref('alert'); // Default notification type is alert
const message = 'Hello, this is a notification!';

const showNotification = () => {
  // Create the Notification abstraction with the selected implementation
  const notification = notificationType.value === 'alert'
    ? new Notification(new AlertNotification())
    : new Notification(new ToastNotification());

  // Show the notification
  notification.show(message);
};
</script>
```

In this example, we have created the `Notification` abstraction and two concrete implementations: `AlertNotification` and `ToastNotification`. The `Notification` class takes an implementation as a constructor parameter and delegates the `show` method to the implementation.

In the `MyComponent.vue`, we have a button that triggers the `showNotification` function. The `showNotification` function creates an instance of the `Notification` abstraction with the selected implementation based on the `notificationType`. It then calls the `show` method on the abstraction, which internally invokes the `show` method of the selected implementation. This allows us to switch between `AlertNotification` and `ToastNotification` without changing the client code.

Now, when you use `MyComponent` in your application, you can easily switch between different notification types by changing the `notificationType` value without modifying the component's code. This demonstrates the decoupling achieved through the Bridge Design Pattern.