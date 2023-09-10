<template>
    <div class="vue-confirm-message">
        <div class="vue-confirm-title" @click.stop="showMessageBox">{{ title || 'Confirm' }}</div>
        <div v-if="show" class="vue-confirm-container" @click="cancel">
            <div class="vue-confirm-main" @click.stop>
                <div class="vue-confirm-msg">{{ message || title || 'Confirm' }}</div>
                <div class="vue-confirm-yes-no-buttons">
                    <span class="confirm-button" @click.stop="confirm">{{ yes || 'Yes' }}</span>
                    <span class="cancel-button" @click.stop="cancel">{{ no || 'No' }}</span>
                </div>
            </div>
        </div>
        <div v-if="show" class="vue-confirm-bg" @click="cancel"></div>
    </div>
</template>

<script>
export default {
  props: [
    'title',
    'message',
    'yes',
    'no',
    'shortcuts'
  ],

  data: () => ({
    show: false
  }),

  beforeDestroy () {
    this.close()
  },

  methods: {
    confirm () {
      this.$emit('confirm')
      this.close()
    },

    cancel () {
      this.$emit('cancel')
      this.close()
    },

    close () {
      if (this.show) {
        this.show = false
        this.clearKeyHook()
      }
    },

    clearKeyHook () {
      if (this.shortcuts) {
        window.removeEventListener('keyup', this.keyUpHandler)
      }
    },

    setKeyHook () {
      if (this.shortcuts) {
        this.clearKeyHook()
        window.addEventListener('keyup', this.keyUpHandler)
      }
    },

    keyUpHandler (e) {
      if (e.code === 'Escape') {
        this.cancel()
      } else if (e.code === 'Enter' || e.code === 'NumpadEnter') {
        this.confirm()
      }
    },

    showMessageBox () {
      if (this.show) {
        this.close()
      } else {
        this.show = true
        this.setKeyHook()
      }
    }
  }
}
</script>

<style scoped>
.vue-confirm-message {
}

.vue-confirm-container {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(249, 249, 249, 0.89);
    z-index: 102;
}

.vue-confirm-container > span {
    background-color: #ffffff;
    padding: 1em;
    border-radius: 0.3em;
    border: 1px solid #e2e2e2;
}

.vue-confirm-main {
    border: 1px solid #838383;
    padding: 2em;
    background: #ffffff;
}

.vue-confirm-bg {
    cursor: pointer;
    z-index: 101;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(255, 255, 255, 0);
}

.vue-confirm-title {
    border: 1px solid #c0c0c0;
    padding: 0 0.2em;
    cursor: pointer;
    font-weight: 700;
    text-align: center;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

.vue-confirm-title:hover {
    border: 1px solid #696969;
}

.vue-confirm-yes-no-buttons {
    display: flex;
    flex-direction: row;
    justify-content: center;
}

.vue-confirm-msg {
    font-size: 1.1em;
    margin-bottom: 0.5em;
}

.confirm-button {
    color: #ffffff;
    background-color: #509f65;
    cursor: pointer;
    text-align: center;
    user-select: none;
    -webkit-user-select: none;
    border: 1px solid #509f65;
    padding: 0.5em;
    margin: 0.5em;
}

.confirm-button:hover {
    color: #509f65;
    background-color: unset;
}

.cancel-button {
    color: #ffffff;
    background-color: #ff0000;
    cursor: pointer;
    text-align: center;
    user-select: none;
    -webkit-user-select: none;
    border: 1px solid #ff0000;
    padding: 0.5em;
    margin: 0.5em;
}

.cancel-button:hover {
    color: #ff0000;
    background-color: unset;
}

.dark .vue-confirm-container {
    background: rgba(58, 57, 57, 0.89);
}

.dark .vue-confirm-main {
    background-color: #2A2A2A;
    color: #f1f1f1;
}
</style>
