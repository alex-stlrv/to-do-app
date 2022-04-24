<template>
<div>
  <h1>To-Do Item</h1>
  <form>
    <label>To-Do</label>
    <input type="text" required v-model="item.name" size="50">

    <label>Priority</label>
    <select v-model='item.priority'>
      <option value=1>High</option>
      <option value=2>Medium</option>
      <option value=3>Low</option>
    </select>
  </form>
  <button @click="addToList">Add Me!</button>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ItemType from '../types/Item' 

export default defineComponent({
  name: 'ToDoItem',
  data () {
    return {
      item: {
        name: '',
        priority: 2,
        done: false,
      } as ItemType,
      nameError: '',
    } 
  },
  methods: {
    addToList() {
      this.nameError = this.item.name === '' ?
        'To-Do Items Cannot Be Empty' : ''
      if (!this.nameError) {
        this.$emit('add', this.item)
      }
    }
  }
});
</script>


<style scoped>

</style>>
