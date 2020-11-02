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
        <div class="field">
          <div class="control">
            <div class="select is-primary is-medium">
              <select v-model="alertAnimation">
                <option value="fade">Fade</option>
                <option value="slide">Slide</option>
              </select>
            </div>
          </div>
        </div>
        <br />
        <button class="button is-primary" @click="show = !show">
          Show Alert
        </button>
        <br />
        <br />
        <transition :name="alertAnimation">
          <div class="notification is-info" v-show="show">
            This is some <info></info>
          </div>
        </transition>
        <transition name="slide" type="animation">
          <div class="notification is-info" v-if="show">This is some info</div>
        </transition>
        <transition
          appear
          enter-active-class="animated bounce"
          leave-active-class="animated shake"
        >
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
      show: true,
      alertAnimation: 'fade'
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

.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  transition: opacity 1s;
}
.fade-leave {
  opacity: 1;
}
.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}
.slide-enter {
  opacity: 0;
}
.slide-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 0.5s;
}
.slide-leave {
}
.slide-leave-active {
  animation: slide-out 1s ease-out forwards;
  transition: opacity 3s;
  opacity: 0;
}

@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0);
  }
}
@keyframes slide-out {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(20px);
  }
}
</style>
