# Adapter

In Vue.js version 3 with script setup, you can implement the Adapter Design Pattern to make components compatible with different data sources or APIs. Here's an example of how to do it:

Let's say we have two different APIs for fetching user data: `OldUserAPI` and `NewUserAPI`, and we want to create a component that can work with both APIs using the Adapter Design Pattern.

1. Create the Adapters and APIs:

```js
<!-- OldUserAPI.js -->
class OldUserAPI {
  getUsers() {
    return Promise.resolve([
      { id: 1, name: 'John Doe' },
      { id: 2, name: 'Jane Smith' },
    ]);
  }
}

<!-- NewUserAPI.js -->
class NewUserAPI {
  fetchUsers() {
    return Promise.resolve([
      { userId: 1, fullName: 'John Doe' },
      { userId: 2, fullName: 'Jane Smith' },
    ]);
  }
}

<!-- UserAdapter.js -->
class UserAdapter {
  constructor(api) {
    this.api = api;
  }

  getUsers() {
    if (this.api instanceof OldUserAPI) {
      return this.api.getUsers().then((users) =>
        users.map((user) => ({ id: user.id, name: user.name }))
      );
    } else if (this.api instanceof NewUserAPI) {
      return this.api.fetchUsers().then((users) =>
        users.map((user) => ({ id: user.userId, name: user.fullName }))
      );
    } else {
      return Promise.reject(new Error('Invalid API'));
    }
  }
}
```

2. Use the Adapter in the component:

```vue
<!-- UserListComponent.vue -->
<template>
  <div>
    <h1>User List</h1>
    <ul>
      <li v-for="user in users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import UserAdapter from './UserAdapter.js';
import OldUserAPI from './OldUserAPI.js';
import NewUserAPI from './NewUserAPI.js';

const users = ref([]);

const oldAPI = new OldUserAPI();
const newAPI = new NewUserAPI();
const adapter = new UserAdapter(oldAPI); // Use the adapter with OldUserAPI by default

onMounted(async () => {
  try {
    // Fetch users using the adapter (works with both OldUserAPI and NewUserAPI)
    users.value = await adapter.getUsers();
  } catch (error) {
    console.error('Error fetching users:', error.message);
  }
});
</script>
```

In this example, we have created `OldUserAPI` and `NewUserAPI`, which represent two different data sources. We also have an `UserAdapter` class that adapts the APIs to a common interface. The `getUsers` method of the `UserAdapter` class handles the conversion of data from the different APIs to a common format.

In the `UserListComponent.vue`, we use the `UserAdapter` with the `OldUserAPI` by default. When the component is mounted, we fetch the users using the adapter, and it will work with both `OldUserAPI` and `NewUserAPI`, making the component compatible with different data sources. You can switch the adapter to use the `NewUserAPI` by replacing `new UserAdapter(oldAPI)` with `new UserAdapter(newAPI)` if needed.