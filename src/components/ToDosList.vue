<template>
    <div>
        <div v-if="activeItems.length">
            <h1>Things To Do</h1>
            <ul v-for="item of activeItems" :key = "item">
                <p>{{ item.name }}</p>
                <p>{{ mappedPriority(item.priority) }}</p>
                <p>
                    <label>Done</label>
                    <input type="checkbox" @click='moveItemToInactive(item.id)'>
                </p>
            </ul>
        </div>
        <div v-if="inactiveItems.length">
            <h1>Deeds Done</h1>
                <ul v-for="item of inactiveItems" :key = "item">
                <p>{{ item.name }}</p>
                <p>{{ mappedPriority(item.priority) }}</p>
                <p>Done</p>
            </ul>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';


export default defineComponent({
  name: 'ToDoItem',
  props: ['activeItems', 'inactiveItems'],
  computed: {
    mappedPriority () {
        return (priority: 1 | 2 | 3 ): string => {
        let response = ''
        if (priority === 1) {
            response = 'High'
        } else if (priority === 2) {
            response = 'Medium'
        } else if (priority === 3) {
            response = "Low"
        }
        return response
        }
    } 
  },
  methods: {
    moveItemToInactive (id: number) {
        this.$emit('move', id)
    }
  }
});
</script>

<style scoped>
ul {
display: flex; /*Targets each list containing the paragraphs*/
padding: 0 20px;
min-height: 50px;
}

ul p {
flex: 0 0 25%; /*This is the sweet sauce*/
}


</style>