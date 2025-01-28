<template>
    <div>
        <div class="rounded bg-neutral-800">
            <div class="text-lg p-1"> Press on the button to get a random Name !</div>
            <div class="flex flex-col justify-center p-3 rounded bg-neutral-600">
              <div>Choose a gender: </div>
              <div class="grid grid-cols-2 gap-4">
                <!-- 
                <input-radio-component :value="'F'" :title="'Female'" />
                <input-radio-component :value="'M'" :title="'Male'" />
                <input-radio-component :value="'NG'" :title="'Gender neutral'" />
                <input-radio-component :value="'nofilter'" :title="'Whatever'" />
                -->

                <div class="bg-indigo-400 rounded-full py-2 px-3 text-indigo-950">
                  <input type="radio" id="Female" value="F" v-model="GenderChoose" />
                  <label for="Female" class="px-2">Female</label>
                </div>
                <div class="bg-indigo-400 rounded-full py-2 px-5 text-indigo-950">
                  <input type="radio" id="Male" value="M" v-model="GenderChoose" />
                  <label for="Male" class="px-2">Male</label>
                </div>
                <div class="bg-indigo-400 rounded-full py-2 px-5 text-indigo-950">
                  <input type="radio" id="Gender neutral" value="NG" v-model="GenderChoose" />
                  <label for="Gender neutral" class="px-2">Gender neutral</label>
                </div>
                <div class="bg-indigo-400 rounded-full py-2 px-5 text-indigo-950">
                  <input type="radio" id="Whatever" value="nofilter" v-model="GenderChoose" />
                  <label for="Whatever" class="px-2">Whatever</label>
                </div>
              </div>
            </div>
            <div class="flex justify-center p-3">
                <button-component :title="ButtonTitle" @click=selectName :disabled="GenderChoose == 'unfiltered'" class="bg-indigo-400 rounded-full py-2 px-5 text-indigo-950 cursor-not-allowed" :class="{'cursor-pointer': GenderChoose !== 'unfiltered'}" />
             </div>
            <div class="flex justify-center pt-8 pb-3" :hidden="GetNameButtonClicked == false"> 
                <div> {{  ChoosenName  }} </div>
            </div>
        </div>
        <div class="flex justify-center p-3">
          <button-component :title="'Restart'" @click=reset class="bg-indigo-500 rounded-full py-2 px-5 text-indigo-950 cursor-pointer" />
         </div>
    </div>
  </template>

<script>
import namesData from '../assets/NamesData.json'
import ButtonComponent from './buttons/ButtonComponent.vue';
import InputRadioComponent from './forms-items/InputRadioComponent.vue';

export default {
  components: {
    ButtonComponent,
    InputRadioComponent
  },
  data() {
    return {
        NamesList: namesData,
        ChoosenName : String,
        ButtonTitle: String,
        GenderChoose: String,
        GetNameButtonClicked: Boolean = false

    }
  },
  created() {
    this.ButtonTitle = "Get a name"
    this.GenderChoose = "unfiltered"
  },
  methods: {
    selectName() {
      console.log(this.GenderChoose)
      let number = 0
      let FiltredNameList = []
        if(this.GenderChoose !== 'nofilter'){
          FiltredNameList = this.NamesList.filter((Name) => Name.gender == this.GenderChoose)
          number = Math.floor(Math.random() * FiltredNameList.length)
          this.ChoosenName = FiltredNameList[number].name
        } else {
          number = Math.floor(Math.random() * this.NamesList.length)
          this.ChoosenName = this.NamesList[number].name
        }
        this.GetNameButtonClicked = true
        this.ButtonTitle = "Get another name"
        
    },
    reset() {
      location.reload();
    }

  }
}

</script>