<script setup lang="ts">

import { ref, onMounted } from 'vue'
let svarighet = 5
let score = 0
    let nyFaktor1 = Math.ceil(Math.random() * 10)
    let nyFaktor2 = Math.ceil(Math.random() * 10)
const tal0 =ref()
const tal = ref( [{
    id: "0",
    faktor1: nyFaktor1,
    faktor2: nyFaktor2,
    summa: nyFaktor1 * nyFaktor2,
    svar: null,
    isCorrect: false,
    isCorrected: false}
   ])

let nextTalId = 0

let nextTalIdString = "1"
let nextFormIdNr = 1
let nextFormNr = 1
let nextFormId = "1"


function focusNext() {
      playAudio ("https://actions.google.com/sounds/v1/cartoon/wood_plank_flicks.ogg")

  let currentFormNr = parseInt(document.activeElement!.id)
  nextFormNr = ++currentFormNr
  nextFormId = nextFormNr.toString();
  if (document.getElementById(nextFormId) != null) { document.getElementById(nextFormId)!.focus(); }
  else { document.getElementById("next-button")!.focus(); }

  score = ++score
}

function reload() {
  window.location.reload(),
  window.scrollTo(0, 0) 
}

function playAudio(url: string | undefined) {
  new Audio(url).play()
}

function addNewTal(this: any) {
    let nyFaktor1 = Math.ceil(Math.random() * 10)
    let nyFaktor2 = Math.ceil(Math.random() * 10)
    nextTalId = ++nextTalId,
    nextTalIdString = nextTalId.toString();
    let s =  
    {
    id: nextTalIdString,
    faktor1: nyFaktor1,
    faktor2: nyFaktor2,
    summa: nyFaktor1 * nyFaktor2,
    svar: null,
    isCorrect: false,
    isCorrected: false
    };
  tal.value.push(s)
 
}

</script>

<template>
  <div class="header card">
    <span>{{ score }} </span><input type="number" class="svarighet" placeholder="svårighetsgrad" v-model="svarighet" />
    <div class="flex">
      <button class = secondary id="refresh-button" @click="reload()">Börja om</button>
     <button id="next-button" @click="addNewTal()">Nytt tal</button>
    </div>

  </div>
  <div class="content">
    <div class="card" :class="{ correct: item.isCorrected }" v-for="item in tal">
      <div class="flex">
        <div class="tal">{{ item.faktor1 }} x {{ item.faktor2 }} </div> = <div class="svar">
          <input type="number" :id="item.id" v-model="item.svar" :disabled="item.isCorrected!" placeholder="svar"
            @input="item.svar == item.summa ? item.isCorrect = true : false"
            @keyup.enter="item.isCorrect ? (item.isCorrected = true, focusNext()) : false" />

        </div>
      </div>

      <button class="secondary" v-if="item.isCorrected == false"
        @click="item.isCorrect ? (item.isCorrected = true, focusNext()) : null">Rätta</button>

      <span v-if="item.isCorrected">Rätt!</span>
    </div>
    

  </div>


</template>
