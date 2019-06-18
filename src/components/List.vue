<template>
  <div>
    <h2>{{ title }}</h2>
    <ul v-bind:class="title | lowercase">
      <li v-for="(task, index) in tasks" v-bind:key="index">
        {{ task.title }}
        <button @click="update(index)">&#10003;</button>
        <button @click="remove(index)">&#10007;</button>
      </li>
    </ul>   
  </div>
</template>

<script>
export default {
  props: [
    'title',
    'tasks'
  ],
  methods: {
    update(index) {
      this.$emit('update', index);
    },    
    remove(index) {
      this.$emit('remove', index);
    }            
  },  
  filters: {
    lowercase: function(value) {
      if(!value) return '';

      return value.toString().toLowerCase();
    }
  }
}
</script>

<style scoped>

</style>
