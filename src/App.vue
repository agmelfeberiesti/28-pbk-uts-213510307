<template>
  <div>
    <h1>TO-DO LIST</h1>
    <form @submit.prevent="addActivity">
      <input type="text" v-model="newActivity" placeholder="Add activity...">
      <button>Add</button>
    </form>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.completed }">
        <input type="checkbox" v-model="activity.completed">
        <span class="satu">{{ activity.text }}</span>
        <button @click="removeActivity(index)">Remove</button>
      </li>
    </ul>
    <div class="show">
      <label>Show only unfinished activities:</label>
      <input type="checkbox" v-model="showUnfinished">
    </div>
  </div>
</template>
<script>
export default{
data(){
  return {
      newActivity: '',
      activities: [
        { text: 'Membaca Buku', completed: false },
        { text: 'Menjahit Baju', completed: true },
        { text: 'Membersihkan Teras Rumah', completed: false }
      ],
      showUnfinished: false
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ text: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    }
  },
  computed: {
    filteredActivities() {
      if (this.showUnfinished) {
        return this.activities.filter(activity => !activity.completed);
      } else {
        return this.activities;
      }
    }
  }
}
</script>

<style>
body {
  background-color: khaki;
  text-align: center;
}
h1 {
  color: brown;
  text-align: center;
}
.done {
  text-decoration: line-through;
}
.show {
  color: black;
}
.satu{
  color: black;
  width: 200px;
}
</style>