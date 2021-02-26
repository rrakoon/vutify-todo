<template>
  <div class="home">
    <!-- Input Task -->
    <v-text-field 
    v-model="newTaskTitle"
    @click:append="addTask"
    @keyup.enter="addTask"
    class="pa-3" 
    outlined 
    label="Add Task" 
    append-icon="mdi-plus-box" 
    hide-details 
    clearable>
    </v-text-field>
    
    <v-list class=" pt-6" flat>
      <!-- <v-list-item-group v-model="settings"> -->
      <div v-for="task in tasks" :key="task.id">
        <v-list-item @click="doneTask(task.id)" :class="{ '#64B5F6': task.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{ 'text-decoration-line-through': task.done }">
                {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="#EF5350">mdi-trash-can-outline</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
      <!-- </v-list-item-group> -->
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      newTaskTitle:'hi',
      tasks: [
        { id: 1, title: "WakeUp", done: false },
        { id: 2, title: "Wash", done: false },
        { id: 3, title: "Do Vue", done: false },
      ],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    delteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask(){
      let newTask ={
        id:Date.now(),
        title:this.newTaskTitle,
        done:false
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    }
  },
};
</script>
