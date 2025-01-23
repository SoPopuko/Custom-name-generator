<template>
    <div class="flex justify-center">
        <div class="rounded bg-neutral-800">
            <div class="text-lg p-1"> Press on the button to get a random Name !</div>
            <div class="flex justify-center p-3">
                <button @click=selectName class="bg-indigo-400 rounded-full py-2 px-5 text-indigo-950 cursor-pointer">{{ ButtonTitle }}</button>
            </div>
            <div class="flex justify-center pt-8 pb-3" :hidden="GetNameButtonClicked == false"> 
                <div> {{  ChoosenName  }} </div>
            </div>
        </div>
    </div>
  </template>

<script>
export default {
  data() {
    return {
        NamesList: Array = ['Louise', 'Edward', 'Kate', 'Ricky', 'Barbara', 'Lewis'],
        ChoosenName : String,
        ButtonTitle: String,
        GetNameButtonClicked: Boolean = false

    }
  },
  created() {
    this.ButtonTitle = "Get a name"
  },
  methods: {
    selectName() {
        const number = Math.floor(Math.random() * this.NamesList.length)
        this.ChoosenName = this.NamesList[number]
        this.GetNameButtonClicked = true
        this.ButtonTitle = "Get another name"
        console.log(this.ChoosenName)
    }

  }
}

</script>