<template>
  <div id="app">
    <h1>My Tasks</h1>
    <form @submit.prevent="create">
      <input type="text" placeholder="e.g. Throw the rubbish" v-model="task">
      <button type="submit">+</button>
    </form>
    <List v-bind:tasks="todos" title="Todo" @update="update" @remove="remove" />
    <List v-bind:tasks="dones" title="Done" @update="update" @remove="remove" />
  </div>
</template>

<script>
import List from './components/List.vue'

export default {
  data() {
    return {
      task: '',
      tasks: [
          {
            title: 'Feed the cat',
            status: 0
          },      
          {
            title: 'Pick up the milk',
            status: 1
          }        
      ]
    }
  },
  computed: {
    todos: function() {
      return this.tasks.filter(function(task) {
        return task.status === 0;
      });
    },    
    dones: function() {
      return this.tasks.filter(function(task) {
        return task.status === 1;
      });
    }
  },
  methods: {
    create() {
      this.tasks.push({ title: this.task, status: 0});
      this.task = '';
    },
    update(index) {
      this.tasks[index].status = 1;
    },    
    remove(index) {
      this.tasks.splice(index, 1);
    }
  },       
  components: {
    List
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto');

html {
    height: 100%;
}

body {
    height: 100%;

    margin: 0;
    padding: 0;

    font-family: 'Roboto';
    font-size: 100%;
}

#app {
    margin: auto;
    padding: 15px;

    width: 100%;
    max-width: 320px;
}

h1, h2 {
  margin: 20px 0 10px 0;
}

input {
  width: 200px;
  height: 30px;

  border: 0;
  border-bottom: 1px solid #000;

  font-size: 100%;
}

button {
  margin: 0 0 0 10px;
  padding: 0;

  width: 15px;
  height: 30px;

  border: 0;
  background-color: #fff;

  font-size: 100%;

  cursor: pointer;
}

ul {
  margin: 0;
  padding: 0;
}

li {
  font-size: 100%;
}

.done li {
  text-decoration: line-through;
}
</style>
