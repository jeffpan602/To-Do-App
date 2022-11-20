<template>
  <div id="app">
    <toDo />
  </div>
</template>

<script>
import toDo from './components/toDo';

export default {
  name: 'App',

  components: {
    toDo,
  },

  data: () => ({
    //
  }),
};
</script>
