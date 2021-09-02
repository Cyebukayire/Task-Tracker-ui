<template>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
</template>


<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'
export default {
    name: 'Home',
    props: {
        showAddTask: Boolean,
    },
    components: {
        Tasks,
        AddTask
    },
    data(){
        return {
            tasks: []
        }
    },
     methods: {

    addTask(task) {
      this.tasks = [...this.tasks, task]
    },

    deleteTask(id) {
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
     
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => 
      task.id === id ? { ...task, reminder: !task.reminder } : task)
    },
  },

  created() {
    this.tasks = [
      {
        "text": "Dentist Appointment",
        "day": "Today 1:30 pm",
        "reminder": false,
        "id": 1
      },
      {
        "text": "Class Project Presentation",
        "day": "tomorrow 4:00 pm",
        "reminder": true,
        "id": 2
      },
      {
        "text": "IELTS Exam",
        "day": "Today 1:30 pm",
        "reminder": true,
        "id": 3
      },
      {
        "text": "Dance",
        "day": "Today 1:30 pm",
        "reminder": false,
        "id": 4
      },
    ]
  },
}
</script>