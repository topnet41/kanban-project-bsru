<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit="create_task_submit"/>
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
          tasks:[
            {
              task_name:"test"
            }
          ]
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
  },methods:{
    create_task_submit(column_index,item){
        this.data[column_index].tasks.push(item);
    }
  }
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
