<template>
  <div class="container">
    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Listado de tareas</h1>
          <h2 class="subtitle">Ejemplo con VueJS</h2>
        </div>
      </div>
    </section>
    <div class="columns">
      <div class="column center">
        <div class="field has-addons">
          <div class="control has-icons-left ">
            <input
              id="inptAnadir"
              v-model="task"
              type="text"
              class="input is-primary is-rounded is-medium"
              placeholder="Agregar nueva tarea"
            />
            <span class="icon is-medium is-left">
              <i class="fas fa-tasks"></i>
            </span>
          </div>
          <div class="control">
            <a
              v-on:click="addTask"
              class="button is-primary is-rounded is-medium"
            >
              <span class="icon is-small"> <i class="fas fa-plus"></i> </span>
              <span>Añadir</span>
            </a>
          </div>
        </div>
      </div>
    </div>
    <hr />
    <h4 class="subtitle">Pendientes</h4>
    <div class="list is-hoverable" v-if="list">
      <a
        class="list-item"
        v-for="(items, index) in list"
        :key="index"
        v-on:click="checkTask(items, index);"
      >
        {{ items.task }}
        <span class="icon check"> <i class="fas fa-check"></i></span>
      </a>
      <a href="#" class="list-item" v-show="list.length === 0"
        >No hay elementos nuevos</a
      >
    </div>
    <br />
    <div v-show="done.length > 0">
      <h4 class="subtitle">Realizadas</h4>
      <div class="list">
        <a class="list-item" v-for="(items, index) in done" :key="index">
          {{ items.task }}
          <span class="icon check"> <i class="fas fa-thumbs-up"></i></span>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      id_task: 1,
      task: "",
      list: [],
      done: []
    };
  },
  methods: {
    addTask: function() {
      this.list.push({
        id: this.id_task,
        task: this.task
      });
      this.task = "";
      this.id_task += 1;
    },
    checkTask: function(item, index) {
      this.done.push({
        id: item.id,
        task: item.task
      });
      this.list.splice(index, 1);
    }
  }
};
</script>

<style>
.container {
  text-align: center;
}

a {
  text-align: left;
}

.check {
  text-align: right !important;
}

.center {
  text-align: center;
}

.center > .field {
  display: inline-flex;
}

#inptAnadir {
  width: 600px;
}
</style>
