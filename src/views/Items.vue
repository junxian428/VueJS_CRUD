<template>
    <div>
      <h1>Items</h1>
  
      <!-- Form for creating new item -->
      <form @submit.prevent="addItem">
        <input v-model="newItemText" type="text" placeholder="Enter item text" required>
        <button type="submit">Add Item</button>
      </form>
  
      <!-- List of items -->
      <ul>
        <li v-for="(item, index) in items" :key="index">
          <span v-if="index !== editIndex">
            {{ item.text }}
            <button @click="editItem(index)">Edit</button>
          </span>
          <span v-else>
            <form @submit.prevent="updateItem">
              <input v-model="items[editIndex].text" type="text" required>
              <button type="submit">Update</button>
              <button @click="cancelEdit">Cancel</button>
            </form>
          </span>
          <button @click="deleteItem(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        items: [],          // Array to store items
        newItemText: '',    // Text for new item
        editIndex: null,    // Index of item being edited (-1 for new item)
      };
    },
    methods: {
      addItem() {
        // Create a new item object and add it to the items array
        const newItem = {
          text: this.newItemText,
        };
        this.items.push(newItem);
  
        // Clear the input field
        this.newItemText = '';
      },
      editItem(index) {
        // Set the editIndex and populate the input field with item text
        this.editIndex = index;
      },
      updateItem() {
        // Clear the editIndex
        this.editIndex = null;
      },
      cancelEdit() {
        // Clear the input field and reset the editIndex
        this.editIndex = null;
      },
      deleteItem(index) {
        // Remove the item at the given index from the items array
        this.items.splice(index, 1);
      },
    },
  };
  </script>
  