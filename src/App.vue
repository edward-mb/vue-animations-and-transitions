<template>
  <div class="container">
    <div class="columns is-mobile is-multiline is-centered">
      <div class="column is-two-thirds has-text-centered">
        <img
          class="image is-128x128 is-inline-block"
          alt="Vue logo"
          src="./assets/logo.png"
        />
      </div>
      <div class="column is-two-thirds">
        <h1 class="is-size-1">Animations</h1>
        <hr />
        <button class="button is-primary" @click="show = !show">
          Show Alert
        </button>
        <br />
        <br />
        <transition>
          <div class="notification is-info" v-if="show">This is some info</div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      show: false
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
