<template>
<div>
  <ToDoItem @add="appendItem"/>
  <ToDosList :activeItems="activeItems" :inactiveItems="inactiveItems" @move="moveItem"/>
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
      activeItems: [] as ItemType[],
      inactiveItems: [] as ItemType[],
    } 
  },
  methods: {
    appendItem (value: ItemType) {
      this.activeItems.push(value)
    },
    moveItem (id: number) {
      console.log(id)
      const todo = this.activeItems.filter(item => item.id === id)
      this.activeItems = this.activeItems.filter(item => item.id !== id)
      this.inactiveItems.push(...todo)
    },

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
