<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],
      tasks: [
        {
          name: "Modul abschliessen",
          status: "to-do",
        },
        {
          name: "SBW Anrufen",
          status: "in-progress",
        },
        {
          name: "ToDo List",
          status: "finished",
        },
      ],
    };
  },
  methods: {
 
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    submitTask() {
      if (this.task.length === 0) return;
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      }
      this.task = "";
    },
  },
};

</script>


<template>
    <div class="container">
        <div class="title">
            <h2>ToDos</h2>
        </div>
        <img src="src/assets/sbw+neue-medien.svg" alt="Italian Trulli">
        <div class="content">
            <div class="form">
                <input type="text" v-model="task">
                <button @click="submitTask">Enter</button>
            </div>
            <div class="todos">
                <table>
                    <thead>
                        <tr>
                            <th scope="col">Task</th>
                            <th scope="col">Status</th>
                            <th scope="col">#</th>
                            <th scope="col">#</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(task, index) in tasks" :key="index">
                            <td>
                                <span :class="{ 'finished': task.status === 'finished' }">
                                 {{ task.name }}
                                </span>
                            </td>
                            <td>
                                <span @click="changeStatus(index)">
                                    {{ task.status }}
                                </span>
                            </td>
                            <td>
                                <div @click="deleteTask(index)">
                                    <span>Löschen</span>
                                </div>
                            </td>
                            <td>
                                <div @click="editTask(index)">
                                    <p>Bearbeiten</p>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<style scoped>

    *{
        font-family: 'Helvetica';
        text-align: center;
        justify-content: center;
        margin: 20px;
    }

    .title{
        text-align: center;
        color: red;
    }
    .todos{
        display: flex;
        justify-content: center;
        text-align: center;
        margin: 5px;
        padding: 10px;
    }
    .th{
        color: aqua;
    display: ;
            }
</style>