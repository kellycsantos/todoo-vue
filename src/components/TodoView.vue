<template>
  <div class="hello">
    <div class="input-container">
      <input
        type="text"
        placeholder="Escreva sua tarefa aqui"
        class="input-task"
        v-model="newTask"
      />
      <input
        type="submit"
        @click="addTask"
        class="button"
        :disabled="disabled"
      />
    </div>

    <div
      v-for="(task, index) in tasks"
      :key="index"
      class="task-row"
      @click="completedTask(task)"
    >
      <span class="status-bar" :style="`background:${task.background}`"></span>
      <span> {{ task.task }}</span>
      <i class="fa fa-trash" aria-hidden="true"></i>
      <span class="status">
        Finalizada?<input type="checkbox" v-model="task.status" />
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoView",
  props: {
    msg: String,
  },
  data() {
    return {
      tasks: null,
      tarefas: [],
      newTask: null,
      check: true,
      disabled: true,
    };
  },
  methods: {
    addTask() {
      if (Array.isArray(this.tasks)) {
        this.tarefas.push({
          task: this.newTask,
          status: false,
          background: "#ff7878",
        });
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
        this.newTask = null;
      }
    },
    completedTask(task) {
      task.status = !task.status;

      if (task.status === true) {
        task.background = "#acff99";
      } else {
        task.background = "#ff7878";
      }
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  watch: {
    newTask(val) {
        if (val !== null && val.length >= 3) {
          return (this.disabled = false);
        } else {
          this.disabled = true;
        }
    },
  },
  mounted() {
    const data = localStorage.getItem("tasks");
    if(data != null || data != undefined){
      this.tasks = JSON.parse(data);
      console.log('Não esta vazio:', data)
      
    } else {
      console.log('vazio')
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
  outline: none;
  box-sizing: border-box;
}
.hello {
  width: 80vw;
  max-width: 600px;
}
.input-task {
  width: 70%;
  height: 35px;
  max-width: 500px;
  margin-right: 5%;
  padding: 5px;
}

.button {
  background: none;
  outline: none;
  height: 35px;
  width: 25%;
  cursor: pointer;
}

.button:disabled {
  cursor: no-drop;
}
.input-container {
  min-height: 5vh;
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
}
.status-bar {
  display: flex;
  height: 100%;
  width: 10px;
  border-radius: 8px;
  border: 0.2px solid #00000065;
}

h1 {
  margin: 60px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.task-row {
  border: 1px solid #1a0000;
  background: rgba(129, 129, 129, 0.116);
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 35px;
  padding: 2.5px 8px;
  margin: 15px 0;
}
</style>
