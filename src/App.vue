<template>
<div>
  <ToDoItem @add="appendItem"/>
  <ToDosList/>
  <ul v-for="item of items" :key = "item">
    <ul v-for="value in item" :key="value"> {{ value }}</ul>
  </ul>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ToDoItem from './components/ToDoItem.vue';
import ToDosList from './components/ToDosList.vue';
import ItemType from './types/Item' 

export default defineComponent({
  name: 'App',
  components: {
    ToDoItem,
    ToDosList,
  },
  data () {
    return {
      items: [] as ItemType[],
    } 
  },
  methods: {
    appendItem (value: ItemType) {
      this.items.push(value)
    }
  }
  
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
