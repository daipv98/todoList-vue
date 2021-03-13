<template>
  <div id="app" class="container">
        <h1></h1>  
        <div class="row cangiua" >
            <input type="text" v-model="selectedTodo.name" class="col-3" placeholder="Task Name">
            <input type="datetime-local" v-model="selectedTodo.deadline" class="col-3" placeholder="Deadline">
            <button v-if="!isEditing" 
                type="button" @click="storeTodo" 
                class="btn btn-success col-1" 
            >Add Task</button>
            <button 
                v-else
                type="button" 
                @click="updateTodo" 
                class="btn btn-success col-1" 
            >Edit Task</button>
        </div>
        <h1 class="text-center">List Todo</h1>

        <input class="col-3 timkiem" type="text" v-model="search" placeholder="Search Task Name">
        <table>
            <tr>
              <th>Task Name</th>
              <th>Deadline</th>
              <th style="width: 160px;">Action</th>
            </tr>
              <items-component v-for="(item, index) in filterList" 
                              :key="index" 
                              :item="item"
                              @msg-index="editTodo(index)"
                              @msg-index2="removeTodo(index)"
                              > 
              </items-component>
          </table>
    </div>
</template>

<script>
import ItemsComponent from './ItemsComponent'


export default {
  name: 'component-todoList',
  data() {
    return {
        isEditing: false,
        todos: [],
        selectedTodo: {},
        selectedIndex: null,
        search: '',
    } 
  },
  
  components: {
    ItemsComponent
  },
    methods: {
        storeTodo() {
            this.todos.push(this.selectedTodo)
            this.selectedTodo = {}
        },

        removeTodo(index) {
            this.todos.splice(index, 1)
        },

        updateTodo() {
            this.todos[this.selectedIndex] = this.selectedTodo;
            this.selectedTodo = {}
            this.isEditing = false
        },
        editTodo(index) {
            this.isEditing = true
            this.selectedTodo = this.todos[index];
            this.selectedIndex = index;
        }, 
        
    },
    computed: {
    filterList() {
      return this.todos.filter(item => {
        return item.name.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  }
}
   
</script>

<style scoped>
.container {
    margin: 0 auto;
}
    .cangiua {
        justify-content: center;
    }
    .timkiem {
        float: right;
        border-radius: 15px;
        margin-bottom: 20px;
    }
    input:focus {
        
    outline:0;
    }
    
    h1 {
        margin: 40px;
    }
    table {
          font-family: arial, sans-serif;
          border-collapse: collapse;
          width: 100%;
        }
        
        td, th {
          border: 1px solid #dddddd;
          text-align: center;
          padding: 8px;
        }
        
        tr:nth-child(even) {
          background-color: #dddddd;
        }
</style>

