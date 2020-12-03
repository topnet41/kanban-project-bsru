<template>
  <div class="kanban">
    <div
      v-for="(item, index) in data"
      :key="index"
      class="colum"
      :style="{ backgroundColor: item.color }">
      <div class="header">
          {{ item.name }}
      </div>
      <div class="bodybox">
          <div class="create-task" @click="create_task(index)">
           + Create Task
        </div>
      </div>
    </div>
    <b-modal ref="create-task-modal" title="Create Task">
        <p class="my-4">Hello from modal!</p>
    </b-modal>
  </div>
</template>

<script>
export default {
    methods:{
        create_task(index){
            console.log(index);
            this.$refs["create-task-modal"].show();
        }
    },
  props: {
    data: Array,
  },
};
</script>

<style>
.kanban {
  width: 100%;
  height: 100%;
  margin: 0px;
  background-color: pink;
}
.colum {
  width: 300px;
  height: 600px;
  margin: 10px;
  padding: 10px;
  border-radius: 10px;
  -webkit-box-shadow: 2px 5px 18px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 2px 5px 18px 0px rgba(0, 0, 0, 0.75);
  box-shadow: 2px 5px 18px 0px rgba(0, 0, 0, 0.75);
  display: inline-block;
}
.header{
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 21px;
    font-weight: bold;
}
.bodybox{
    height: calc(100% - 50px);
    border-radius: 10px;
    padding: 5px;
    background-color: rgba(255, 255, 255, 0.2);
}
.create-task{
    width: 100%;
    height: auto;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
}.create-task:hover{
    background-color: rgba(128, 0, 128, 0.459);
    color: white;
}
</style>