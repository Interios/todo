<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="form-todo">
      <h3>Введите название нового todo и нажмите "Enter"</h3>
      <br>
      <input type="text" @keyup.enter="handleAddToDo" v-model="fieldToDo" />
    </div>
    <div>
      <ToDo v-for="(item, i) in ToDolist" :key="i" :title="item.title" @remove="removeToDo(i)" />
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data: () => ({
    ToDolist: [],
    fieldToDo: ''
  }),
  components: {
    ToDo: () => import('./components/List.vue')
  },
  methods: {
    handleAddToDo() {
      this.ToDolist.push({
        title: this.fieldToDo
      });
      this.fieldToDo = '';
    },
    removeToDo(index) {
      this.ToDolist.splice(index, 1);
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 600px;
  margin: auto;
}
.row{
  display: flex;
  flex-flow: row wrap;
  margin-left: -15px;
  margin-right: -15px;
}

.row:after, .row-before {
  display: table;
  content: "";
}

.col-md-6 {
  width: 50%;
  padding: 0 15px;
}
.form-todo input{
  padding: 10px;
}
</style>
