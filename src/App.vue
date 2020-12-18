<template>
  <div id="app">
    <Header></Header>
    {{ title }}
    <div>
      <b-jumbotron
        header="BootstrapVue"
        lead="Bootstrap v4 Components for Vue.js 2"
      >
        <p>For more information visit website</p>
        <b-button variant="primary" href="#">More Info</b-button>
      </b-jumbotron>
    </div>

    <img alt="Vue logo" src="./assets/logo.png" />

    <div>
      <input v-model="newTaskName" type="text" />
      <b-button @click="addNewTask()">Añadir</b-button>
    </div>
    <div>
      <div v-for="task in tasks" :key="task.id" class="tasks-list">
        <b-row style="padding-left:800px">
        <div @click="markAsDone(task.id)" v-if="!task.completed">
          {{ task.name }}
        </div>
        <div @click="markAsDone(task.id)" v-if="task.completed" class="done">
          {{ task.name }}
        </div>
        <b-button @click="deleteTask(task.id)">Eliminar</b-button>
        </b-row>
      </div>
    </div>

    <Footer></Footer>
  </div>
</template>

<script>
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
  methods: {
    addNewTask() {
      if (this.newTaskName.length > 0) {
        this.tasks.push({
          id: this.tasks.length,
          completed: false,
          name: this.newTaskName,
        });
      }
      this.newTaskName = "";
    },
    markAsDone(id) {
      this.tasks.forEach((task) => {
        if (task.id == id) {
          task.completed = true;
        }
      });
    },
    deleteTask(id) {
      for (let i = 0; i < this.tasks.length; i++) {
        if (this.tasks[i].id === id) {
          this.tasks.splice(i, 1);
        }
      }
    },
  },
  data() {
    return {
      title: "Esto es un title desde vue",
      newTaskName: "",
      tasks: [
        { id: 0, completed: false, name: "Crear publicacion" },
        { id: 1, completed: false, name: "Publicarla" },
        { id: 2, completed: false, name: "Hacerme Rico" },
        { id: 3, completed: false, name: "Otra tarea" },
        { id: 4, completed: false, name: "Una tarea mas" },
      ],
    };
  },
};
</script>


<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
  color: lightgreen;
}

.tasks-list {
  display: inline;
}

</style>
