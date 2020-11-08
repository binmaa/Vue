<template>
  <div @click="sayHello">
      app
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: ''
    }
  },
  methods: {
    sayHello(){
        alert("say hello");
    }
  }
}
</script>

<style scoped>

</style>
