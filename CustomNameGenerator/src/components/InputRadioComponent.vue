<template>
    <div class="bg-indigo-400 rounded-full py-2 px-3 text-indigo-950">
        <input type="radio" :id="title" :value="valueRadio" v-model="GenderChoose" />
        <label :for="title" class="px-2">{{ title }}</label>
    </div>
</template>

<script>
export default {
  props: {
    valueRadio: String,
    title: String
  }
}
</script>