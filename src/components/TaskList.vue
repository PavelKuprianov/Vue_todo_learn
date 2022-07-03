<template>
  <div class="list">
    <div class="item" :class="{done: task.done}" v-for="task in tasks" :key="task.text">
      <input type="checkbox" v-model="task.done">
      {{ task.text }}
      <LikeButton :counter.sync="task.likes" :counterDis.sync="task.dislikes"></LikeButton>
    </div>
  </div>
</template>

<script>
import LikeButton from "@/components/LikeButton";
export default {
  name: "TaskList",
  components: {LikeButton},
  props: ['tasks'],
}
</script>

<style scoped>

</style>