<template>
  <div class="kanban">
    <div
      v-for="(item, index) in data"
      :key="index"
      class="colum"
      :style="{ backgroundColor: item.color }"
    >
      <div class="header">
        {{ item.name }}
      </div>
      <div class="bodybox">
        <div v-for="(task, task_index) in item.tasks" :key="task_index">
          <div
            class="task"
            :draggable="true"
            @dragstart="start_move(task_index, index)"
          >
            <span style="color: white">{{ task.task_name }}</span>
          </div>
        </div>
        <div
          class="drop_zone"
          @dragenter.prevent="drop_zone_enter"
          @dragleave.prevent="drop_zone_leave"
          @dragover.prevent
        ></div>

        <div class="create-task" @click="create_task(index)">+ Create Task</div>
      </div>
    </div>
    <b-modal ref="create-task-modal" title="Create Task">
      <input
        class="input-task-name"
        v-model="task_name"
        @keyup.13="submit_create_task"
      />
    </b-modal>
  </div>
</template>

<script>
export default {
  methods: {
    create_task(index) {
      this.$refs["create-task-modal"].show();
      this.current_column_index = index;
    },
    submit_create_task() {
      this.create_task_submit(this.current_column_index, {
        task_name: this.task_name,
      });
    },
    start_move(task_index, colum_index) {
      this.current_colum_index = colum_index;
      this.create_task_submit = task_index;
    },
    drop_zone_enter(event) {
      event.target.style.height = "100px";
      event.target.style.borderStyle = "dotted";
      event.target.style.transition = "height 0.5s";
    },
    drop_zone_leave(event) {
      event.target.style.height = "10px";
      event.target.style.borderStyle = "none";
      event.target.style.transition = "height 0.5s";
    },
  },
  data() {
    return {
      task_name: "",
      current_column_index: "",
      current_task_index: "",
    };
  },
  props: {
    data: Array,
    create_task_submit: Function,
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
.header {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 21px;
  font-weight: bold;
}
.bodybox {
  height: calc(100% - 50px);
  border-radius: 10px;
  padding: 5px;
  background-color: rgba(255, 255, 255, 0.2);
}
.create-task {
  width: 100%;
  height: auto;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}
.create-task:hover {
  background-color: rgba(128, 0, 128, 0.459);
  color: white;
}
.input-task-name {
  width: 100%;
}
.task {
  position: relative;
  width: auto;
  height: 100px;
  border-radius: 5px;
  margin: 10px;
  background-color: black;
}
.drop_zone {
  height: 10px;
}
</style>