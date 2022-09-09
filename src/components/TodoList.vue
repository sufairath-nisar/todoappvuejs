<template>
  <body>
    <div class="container">
      <div class="main-box border-box rounded align-items-center  m-3">
        <!-- title -->
        <h2 class="title font-weight-bold mb-4 text-center">TODO LIST</h2>
        

        <!-- New todo-->
        <div class="row">
          <div class="col-md-12">
            <input type="text" class="todo-input w-100 mb-3" placeholder="Enter New Items and Press Enter Key" v-model="newItem" @keyup.enter="add">
          </div>
        </div>

        <div class="main-container">
          <div>
            <!-- <button :class="{ active: filter == 'active' }" @click="filter = 'active'">active</button>
            <button type="button" class="btn btn-dark" @click="filter = 'all'">All</button> -->
            <nav class="navbar navbar-expand-sm px-2 bg-light justify-content-center">
              <ul class="navbar-nav">
                <li class="nav-item">
                  <a  :class="{ active: filter == 'all' }"  class="nav-link" @click="filter = 'all'">All</a>
                </li>
             
                <li class="nav-item">
                    <a  :class="{ active: filter == 'active' }" class="nav-link" @click="filter = 'active'">Remaining Items</a>
                </li>

                <li class="nav-item">
                  <a  :class="{ active: filter == 'completed' }" class="nav-link" @click="filter = 'completed'">Selected Items</a>
                </li>
               
              </ul>
            </nav>
          </div>

          <form class="pt-4">
            <div v-for="(todo, index) in todosFiltered" :key="todo.id" >
              <div class="row pb-3">
                <div class="col-md-6 col-lg-6 col-xl-6 col-sm-6 col-8">
                  <input  type="checkbox"  class="checkbox me-2" v-model="todo.completed" >
                  <label>{{ todo.title }}</label>
                </div>
            
              <!--Delete-->
                <div class="col-md-6 col-lg-6 col-xl-6 col-sm-6 col-4">
                  <div class="remove-cls" @click="remove(index)">
                    <i class="fa fa-trash text-center" ></i>
                  </div>
                </div>
              </div>
            </div>
          </form>  
      
          <div class="main-container">
            <div class="mt-4">
              <label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos"> Check All</label>
            </div>
            <div>
              <span class="badge bg-success pb-2 mt-2">{{ remain }} items left</span>
            </div>
          </div>

        </div>    
      </div>
    </div>
  </body>
</template>

<!--script-->
<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newItem: '',
      idnextTodo: 6,
      filter: 'all',
      todos: [
        {
          'id': 1,
          'title': 'Orange',
          'completed': false,
        },
        {
          'id': 2,
          'title': 'Tomato',
          'completed': false,
        },
        {
          'id': 3,
          'title': 'Onion',
          'completed': false,
        },
        {
          'id': 4,
          'title': 'Potato',
          'completed': false,
        },
        {
          'id': 5,
          'title': 'Egg',
          'completed': false,
        }
      ]
    }
  },
  //Remaining items
  computed: {
    remain() {
      return this.todos.filter(todo => !todo.completed).length
    },
    anyRemaining() {
      return this.remain != 0
    },
    todosFiltered() {
      if (this.filter == 'all') {
        return this.todos
      } else if (this.filter == 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter == 'completed') {
        return this.todos.filter(todo => todo.completed)
      }

      return this.todos
    },
    showClearCompletedButton() {
      return this.todos.filter(todo => todo.completed).length > 0
    }
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    add() {
      if (this.newItem.trim().length == 0) {
        return
      }

      this.todos.push({
        id: this.idnextTodo,
        title: this.newItem,
        completed: false,
      })

      this.newItem = ''
      this.idnextTodo++
    },
   
    remove(index) {
      this.todos.splice(index, 1)
    },
    checkAllTodos() {
      this.todos.forEach((todo) => todo.completed = event.target.checked)
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  }
}
</script>

<!--style-->
<style>
.active{
  background-color: rgba(245, 65, 65, 0.884);
  color:rgb(245, 245, 248) !important;
}
</style>