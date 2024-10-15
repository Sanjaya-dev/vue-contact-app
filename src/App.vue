<script setup lang="ts">
import { ref } from 'vue'

const formInput = ref({
  name: '',
  phone: ''
})

const dataContact = ref([
  {
    id: 1,
    name: 'abdul',
    phone: '123456789'
  },
  {
    id: 2,
    name: 'ahmad',
    phone: '12345'
  }
])

function addContact() {
  dataContact.value.push({
    id: dataContact.value.length + 1,
    name: formInput.value.name,
    phone: formInput.value.phone
  })
}

function deleteContact(id : number) {
  dataContact.value = dataContact.value.filter((contact) => contact.id !== id)
}

function editContact(id : number) {
  const contact = dataContact.value.find((contact) => contact.id === id)
  if (contact) {
    formInput.value.name = contact.name
    formInput.value.phone = contact.phone
  }
}

</script>

<template>
  <h1>Hello World</h1>
  <form @submit.prevent="addContact">
    <input type="text" placeholder="name" v-model="formInput.name" />
    <input type="text" placeholder="phone" v-model="formInput.phone" />
    <button>Add Contact</button>
  </form>
  <ul>
    <li v-for="contact in dataContact" :key="contact.id">
      <p>{{ contact.name }}</p>
      <p>{{ contact.phone }}</p>
      <button @click="editContact(contact.id)">Edit</button>
      <button @click="deleteContact(contact.id)">Delete</button>
    </li>
  </ul>
</template>

