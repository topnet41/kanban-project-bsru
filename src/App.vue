<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit="create_task_submit" :move_item_task="move_item_task"/>
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
  },methods:{
    create_task_submit(column_index,item){
        this.data[column_index].tasks.push(item);
    },
    move_item_task(column_a,index_task_a,colum_b,index_task_b){
        var item = this.data[column_a].tasks[index_task_a];

        this.data[column_a].tasks.splice(index_task_a,1)

        this.data[colum_b].tasks.splice(index_task_b,0,item)

    }
  }
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
