<template>
  <div id="app">
    <h1>Contact List</h1>
    <button @click="addRandomContact">Add Random Contact</button>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won an Oscar</th>
          <th>Won an Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in contacts" :key="contact.id">
          <td><img :src="contact.pictureUrl" alt="contact.name" height="100"></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity }}</td>
          <td>{{ contact.wonOscar ? '🏆' : '' }}</td>
          <td>{{ contact.wonEmmy ? '🏆' : '' }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { ref } from 'vue';
import contactsData from './contacts.json';

export default {
  name: 'App',
  setup() {
    const contacts = ref(contactsData.slice(0, 5));

    const addRandomContact = () => {
      const remainingContacts = contactsData.filter(contact => !contacts.value.includes(contact));
      if (remainingContacts.length === 0) return;
      const randomContact = remainingContacts[Math.floor(Math.random() * remainingContacts.length)];
      contacts.value.push(randomContact);
    };

    const sortByName = () => {
      contacts.value.sort((a, b) => a.name.localeCompare(b.name));
    };

    const sortByPopularity = () => {
      contacts.value.sort((a, b) => b.popularity - a.popularity);
    };

    return { contacts, addRandomContact, sortByName, sortByPopularity };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin: 20px 0;
  background-color: #f9f9f9;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

th, td {
  border: 1px solid #ddd;
  padding: 12px;
}

th {
  background-color: #4CAF50;
  color: white;
}
</style>
