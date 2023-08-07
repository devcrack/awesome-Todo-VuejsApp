<template>
  <div class="home">
    <v-text-field
        v-model="newTaskTitle"
        @click:append="addTask"
        @keyup.enter="addTask"
        class="pa-3"
        outlined
        label="Add Task"
        append-icon="mdi-plus"
        hide-details
          ></v-text-field>
    <div v-if="tasks.length">
     <v-list
      class="pt-0"
         flat
    >
       <div
       v-for="task in tasks"
        :key="task.id">
         <v-list-item
         @click="doneTask(task.id)"
         :class="{'blue lighten-5': task.done}"
         >
          <template v-slot:default="{ active, }">
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{'text-decoration-line-through': task.done}">
                {{task.title}}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
          <v-btn icon
          @click.stop="deleteTask(task.id)"
          >
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
        </v-list-item>
         <v-divider></v-divider>
       </div>
    </v-list>
    </div>
    <div v-else
    class="">
      <v-icon
      size="50"
      color="primary">
        mdi-check
      </v-icon>
      <div class="text-h5 primary--text">
        No tasks
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data() {
      return {
        newTaskTitle : '' ,
        tasks:[
      //     {
      //       id: 1,
      //       title: "Wake Up",
      //       done: false
      //     },
      //     {
      //       id: 2,
      //       title: "Get Bananas",
      //       done: false
      //     },
      //     {
      //       id: 3,
      //       title: "Eat Bananas",
      //       done: false
      //     }
        ]
      }
    },
    methods: {
      getTask(id) {
        return this.tasks.filter(task => task.id === id)[0];
      },
      doneTask(id) {
        let task = this.getTask(id);

        task.done = !task.done;
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id != id);

      },
      addTask(){
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        };
        this.tasks.push(newTask);
        this.newTaskTitle = '';
      }
    }
  }
</script>
<style lang="sass">
.no
</style>