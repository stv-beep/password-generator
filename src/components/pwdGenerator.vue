<template>
  <h1 class="title-stv-beep font-mono font-bold text-4xl text-center bg-clip-text text-transparent bg-gradient-to-r from-slate-100 via-slate-300 to-slate-700 mt-14">Random Password Generator</h1>
  <div class="justify-center items-center p-2 m-2 text-center">
    <div class="content-center bg-zinc-800 font-mono justify-center items-center rounded-xl mx-2 my-6 py-3 text-white hover:text-amber-700 
	hover:bg-amber-100 hover:cursor-pointer hover:border-amber-300 border-4 border-zinc-800 m-9 font-bold text-2xl 
  xl:text-4xl md:text-3xl sm:text-2xl" v-on:click="copy(password)" :value="password">{{password || msg}}</div>
    <div class="bg-zinc-800 font-mono justify-center rounded-xl m-2 p-4">
		  <span class="text-white text-lg">Select length </span>
      <input type="range" class="ease-out duration-300 bg-gray-200 rounded-lg w-40 appearance-none cursor-pointer dark:bg-amber-500 active:bg-amber-500 focus:ring-0" :min="min" :max="max" v-model="value" v-on:click="generatePassword(this.value)">
      <input type="number" class="text-center bg-zinc-800 text-amber-500 text-3xl" :min="min" :max="max" v-model="value" readonly disabled>
	    <button type="button" class="ease-out duration-300 rounded-md font-bold bg-gray-100 hover:bg-amber-200 hover:text-amber-700 active:bg-amber-300 m-6 px-32 py-2 xl:text-2xl md:text-xl sm:text-lg" v-on:click="generatePassword(this.value)">Generate</button>
    </div>
    <alert-msg v-if="showMessage" :message="message"/>
  </div> 
</template>

<script>
import AlertMsg from './AlertMsg.vue'

const MIN_LENGTH = 6
const MAX_LENGTH = 25
const DEFAULT_VALUE = 8
const beforePwd = 'Password here...'
const chars = '0123456789abcdefghijklmnopqrstuvwxyz!@#$%^&*()ABCDEFGHIJKLMNOPQRSTUVWXYZ'

export default {
  components: { AlertMsg },
  name: 'pwdGenerator',
  data() {
    return {
      password: '', value: DEFAULT_VALUE, msg: beforePwd, min: MIN_LENGTH, max: MAX_LENGTH, 
      message: 'Password copied!', showMessage: false
    }
  }, 
  methods: {
    generatePassword(length) {
      this.password = ''
      for (let i = 0; i <= length; i++) {
        let randomNumber = Math.floor(Math.random() * chars.length)
        this.password += chars.substring(randomNumber, randomNumber +1)
      }
    },
    async copy(password) {
      if (password !== '' ) {
        await navigator.clipboard.writeText(password)
        this.showMessage = true
        const messageTimeout = window.setTimeout(() => {
          this.showMessage = false
          window.clearTimeout(messageTimeout)
		    }, 2000)
      } 
    }
  }
}
</script>

<style scoped>
  .title-stv-beep{
		text-shadow: rgb(255 215 77 / 40%) -1px -1px 6px, rgb(124 127 255 / 60%) 1px 1px 6px
	}
</style>