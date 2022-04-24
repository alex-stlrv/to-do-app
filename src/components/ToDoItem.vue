<template>
<div>
  <h1>To-Do Item</h1>
  <form>
    <label>To-Do</label>
    <input type="text" required v-model="item.name" size="50">
    <div v-if="nameError">{{ nameError }}</div>

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
        id: 1,
      } as ItemType,
      nameError: '',
    } 
  },
  methods: {
    addToList() {
      if (this.item.name === '') {
        this.nameError = 'To-Do Items Cannot Be Empty'
      } else {
        this.item.priority= Number(this.item.priority) as 1 | 2 | 3
        this.$emit('add', Object.assign({}, this.item))        
        this.nameError = ''        
        this.item.id++
        this.item.name = ''
      }
    },
  }
});
</script>


<style scoped>

form label {
  margin: 20px;
  font-weight: bold;
}

form input {
  margin: 20px;
  font-size: 0.9rem;
}

form select {
  font-size: 0.9rem;
  margin: 20px
}

button {
  font-size: 0.9rem;
}

</style>>
