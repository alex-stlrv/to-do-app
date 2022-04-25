<template>
    <div class="list">
        <div v-if="activeItems.length">
            <h1>Things To Do</h1>
            <div class="sort">
                <button @click="prioritySorted">Sort by Priority</button>
                <button @click="nameSorted">Sort by Name</button>
            </div>
            <ul>
                <li v-for="item of activeItemsCopy" :key = "item">
                    <p class="name">{{ item.name }}</p>
                    <p class="priority">{{ mappedPriority(item.priority) }}</p>
                    <p class="done">
                        <label class="checkbox">Done</label>
                        <input class="checkbox" type="checkbox" @click='moveItemToInactive(item.id)'>
                    </p>
                </li>
            </ul>
        </div>
        <div v-if="inactiveItems.length">
            <h1>Done Deeds</h1>
               <ul>
                    <li v-for="item of inactiveItems" :key = "item">
                        <p class="name">{{ item.name }}</p>
                        <p class="priority">{{ mappedPriority(item.priority) }}</p>
                        <p class="done">Done</p>
                    </li>
            </ul>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ItemType from '../types/Item' 

export default defineComponent({
  name: 'ToDoItem',
  props: ['activeItems', 'inactiveItems'],
  data () {
    return {
        activeItemsCopy: [] as ItemType[],
    }
  },
  watch: {
    'activeItems': {
      handler(activeToDoItems: ItemType[]) {
        this.activeItemsCopy = [...activeToDoItems]
      },
      immediate: true,
      deep: true,
    }
  },
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
    },
    prioritySorted () {
        this.activeItemsCopy.sort(this.priorityRank)
    },
    nameSorted () {
        this.activeItemsCopy.sort(this.nameRank)
    },
    priorityRank(a: ItemType, b: ItemType): -1 | 0 | 1 {
        let result = 0 as -1 | 0 | 1
        if (a.priority > b.priority) {
            result = 1
        } else if (a.priority < b.priority) {
            result = -1 
        }
        return result
    },
    nameRank(a: ItemType, b: ItemType): -1 | 0 | 1 {
        let result = 0 as -1 | 0 | 1
        if (a.name > b.name) {
            result = 1
        } else if (a.name < b.name) {
            result = -1 
        }
        return result
    }
  }
});
</script>

<style scoped>
.list {
    max-width: 800px;
    margin: auto;
}

.sort {
    display: flex; /*Targets each list containing the paragraphs*/
    align-items: center; 
    max-width: 400px;
    margin: auto;   
}

.sort button {
    flex: 0 0 50%;
    margin: 0px 10px;
    font-size: 0.9rem;
}

ul {
    padding: 0;
    border: 1px solid #ddd;
}

li {
    display: grid;
    grid-template-columns: 70% 15% 15%;
    grid-template-areas: "name priority done";
    padding: 0px 20px;
    border-bottom: 1px solid #ddd;
}

.name {
    grid-area: name;
    text-align: left;
}

.priority {
    grid-area: priority;    
    text-align: left;
}

.done {
    grid-area: done;    
    text-align: left;
}

h1 {
    margin-top: 60px;
    margin-bottom: 20px;
}

.checkbox {
    padding: 0px 2px;
    margin: 0px 2px;
}

</style>