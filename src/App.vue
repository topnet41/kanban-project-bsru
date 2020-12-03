<template>
  <div id="app">
    <Kanban :data="data"/>
  </div>
</template>

<script>
import Kanban from "./components/Kanban.vue";

export default {
  name: "App",
  components: {
    Kanban,
  },
  data() {
    return {
      data: [
        {
          name: "todo",
          color: "#3e84c9",
          tasks:[]
        },
        {
          name: "doing",
          color: "#a062c4",
          tasks:[]
        },
        {
          name: "done",
          color: "#e03487",
          tasks:[]
        },
      ],
    };
  },
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
