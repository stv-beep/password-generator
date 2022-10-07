<template>
  <div class="title-stv-beep content-center bg-green-300 font-bold justify-center items-center rounded-xl mx-2 my-6 py-3 text-green-900 hover:text-green-800 
	border-4 border-zinc-800 m-9">{{ message }}
  </div>
</template>

<script>
export default {
  name: 'AlertMsg',
  props: {
    message: String
  }
}
</script>
