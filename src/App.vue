<template>
  <div id="app">
    <h1>Список задач   <LikeButton :counter.sync="headerLikes" :counterDis.sync="headerDisLikes"></LikeButton></h1>
    <h3>Общее количесво лайков на странице - {{ countLikes }}</h3>
    <h3>Общее количесво дизлайков на странице - {{ countDisLikes }}</h3>
    <div v-if="count == 0">Вы великолепны!</div>
    <div v-else-if="count == 1">Надо сделать последний рывок!</div>
    <div v-else>Осталось сделать задач: <span class="counter">{{ count }}</span></div>

    <div v-show="count !== 0">
      <h2>Нерешенные задачи</h2>
      <TaskList :tasks="uncompletedTasks"></TaskList>
    </div>

    <form class="form" @submit.prevent="addTask">
      <input v-model="message">
      <button :type="type">Добавить</button>
      <LikeButton :counter.sync="formLikes" :counterDis.sync="formDisLikes"></LikeButton>
    </form>

    <transition name="bounce">
      <img src="https://ic.pics.livejournal.com/school_28_2016/78375967/25672/25672_100.jpg" v-show="count == 0" alt="Картинка">
    </transition>

    <h2 v-show="completedTasks.length !== 0">Завершённые задачи</h2>
    <TaskList :tasks="completedTasks"></TaskList>

  </div>
</template>

<script>
  import LikeButton from "@/components/LikeButton";
  import TaskList from "@/components/TaskList";
  export default {
    name: 'App',
    components: {TaskList, LikeButton},
    data() {
      return {
        headerLikes: 0,
        headerDisLikes: 0,
        formLikes: 0,
        formDisLikes: 0,
        type: 'submit',
        message: 'Новая задача',
        tasks: [
          {text: 'Развернуть окружение в Codepen', done: true, likes: 0, dislikes: 0},
          {text: 'Пройти курс по Vue', done: false, likes: 0, dislikes: 0},
          {text: 'Сделать интернет-магазин на Vue', done: false, likes: 0, dislikes: 0},
        ],
        title2: 'Завершённые задачи',
      }
    },
    methods: {
      addTask(){
        this.tasks.push({text: this.message, done: false, likes: 0, dislikes: 0});
        this.message='';
      },
    },
    computed: {
      count() {
        return this.tasks.filter(task => !task.done).length;
      },
      completedTasks() {
        return this.tasks.filter(task => task.done);
      },
      uncompletedTasks() {
        return this.tasks.filter(task => !task.done);
      },
      countLikes() {
        return this.headerLikes + this.formLikes + this.tasks.reduce((value, task) => value + task.likes, 0);
      },
      countDisLikes() {
        return this.headerDisLikes + this.formDisLikes + this.tasks.reduce((value, task) => value + task.dislikes, 0);
      }
    }
  }
</script>

<style scoped>

</style>
