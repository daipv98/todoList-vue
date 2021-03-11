<template>
  <div id="app" class="container">
        <h1>Todo App</h1>
        
            
        
        <div class="row cangiua" >
            <input type="text" v-model="selectedTodo.name" class="col-3" placeholder="Task Name">
            <input type="datetime-local" v-model="selectedTodo.deadline" class="col-3"placeholder="Deadline">
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

        <input class="col-4 timkiem" type="text" v-model="search" placeholder="Search">
        <table>
            <tr>
              <th>Task Name</th>
              <th>Deadline</th>
              <th style="width: 160px;">Action</th>
            </tr>
            <tr v-for="(item, index) in filterList">
              <td>{{ item.name }}</td>
              <td>{{ item.deadline }}</td>
              <th>
                <button @click="editTodo(index)" class="btn btn-warning">Edit</button>
                <button @click="removeTodo(index)" class="btn btn-warning" style="background-color: red;">Delete</button>
              </th>
            </tr>
          </table>



        <!-- <ol>
            <li v-for="(item, index) in todos">
                <span>Task name: {{ item.name }}</span>
                <span>Deadline: {{ item.deadline }}</span>
                <button @click="editTodo(index)" class="btn btn-warning">Edit</button>
                <button @click="removeTodo(index)" class="btn btn-warning" style="background-color: red;">Delete</button>
            </li>
        </ol> -->
    </div>
</template>

<script>
export default {
  name: 'component-todoList',
  data() {
    return {
        isEditing: false,
            todos: [],
            selectedTodo: {},
            selectedIndex: null,
            search: ''
    }
    
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
        }
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
        float: left;
        border-radius: 10px;
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

