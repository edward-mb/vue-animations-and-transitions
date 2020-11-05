<template>
  <div class="container">
    <div class="columns is-mobile is-multiline is-centered">
      <div class="column is-two-thirds has-text-centered">
        <img
          class="image is-64x64 is-inline-block"
          alt="Vue logo"
          src="./assets/logo.png"
        />
      </div>
      <div class="column is-two-thirds">
        <h1 class="is-size-2">Animations</h1>
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
            This is some info
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
        <transition :name="alertAnimation" mode="out-in">
          <div class="notification is-info" v-if="show" key="info">
            This is some Info
          </div>
          <div class="notification is-warning" v-else key="warning">
            This is some Warning
          </div>
        </transition>
        <hr />
        <button class="button is-primary" @click="load = !load">
          Load / Remove Element
        </button>
        <br />
        <br />
        <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"
          @before-leave="beforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
          :css="false"
        >
          <div
            style="width: 300px; height: 100px; background-color: lightgreen"
            v-if="load"
          ></div>
        </transition>
        <hr />
        <button
          class="button is-primary"
          @click="
            selectedComponent == 'app-success-alert'
              ? (selectedComponent = 'app-danger-alert')
              : (selectedComponent = 'app-success-alert')
          "
        >
          Toogle Components
        </button>
        <br />
        <br />
        <transition name="fade" mode="out-in">
          <component :is="selectedComponent"></component>
        </transition>
        <hr />
        <button class="button is-primary" @click="addItem">Add Item</button>
        <br />
        <br />

        <ul class="panel">
          <transition-group name="slide">
            <li
              class="panel-block"
              v-for="(number, index) in numbers"
              :key="number"
              @click="removeItem(index)"
              style="cursor: pointer"
            >
              {{ number }}
            </li>
          </transition-group>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import DangerAlert from './DangerAlert.vue'
import SuccessAlert from './SuccessAlert.vue'
export default {
  data () {
    return {
      show: false,
      load: true,
      alertAnimation: 'fade',
      elementWidth: 100,
      selectedComponent: 'app-success-alert',
      numbers: [1, 2, 3, 4, 5]
    }
  },
  methods: {
    beforeEnter (el) {
      console.log('beforeEnter')
      this.elementWidth = 100
      el.style.width = this.elementWidth + 'px'
    },
    enter (el, done) {
      console.log('enter')
      let round = 1
      const interval = setInterval(() => {
        el.style.width = this.elementWidth + round * 10 + 'px'
        round++
        if (round > 20) {
          clearInterval(interval)
          done()
        }
      }, 20)
    },
    afterEnter () {
      console.log('afterEnter')
    },
    enterCancelled () {
      console.log('enterCancelled')
    },
    beforeLeave (el) {
      console.log('beforeLeave')
      this.elementWidth = 300
      el.style.width = this.elementWidth + 'px'
    },
    leave (el, done) {
      console.log('leave')
      let round = 1
      const interval = setInterval(() => {
        el.style.width = this.elementWidth - round * 10 + 'px'
        round++
        if (round > 20) {
          clearInterval(interval)
          done()
        }
      }, 20)
    },
    afterLeave () {
      console.log('afterLeave')
    },
    leaveCancelled () {
      console.log('leaveCancelled')
    },
    addItem () {
      const pos = Math.floor(Math.random() * this.numbers.length)
      this.numbers.splice(pos, 0, this.numbers.length + 1)
    },
    removeItem (index) {
      this.numbers.splice(index, 1)
    }
  },
  components: {
    appDangerAlert: DangerAlert,
    appSuccessAlert: SuccessAlert
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
  transition: opacity 1s;
  opacity: 0;
  position: absolute;
}
.slide-move {
  transition: transform 1s;
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
