<template>
  <div>
    <button type="button" @click="increment">&#9829; {{ counter }}</button>
    <button type="button" @click="incrementDis">&#128078;&#127999; {{ counterDis }}</button>
  </div>
</template>

<script>
export default {
  name: "LikeButton",
  props: ['counter', 'counterDis'],
  methods: {
    increment() {
      this.$emit('update:counter', this.counter + 1);
    },
    incrementDis() {
      this.$emit('update:counterDis', this.counterDis + 1);
    }
  },
}
</script>

<style scoped>

</style>