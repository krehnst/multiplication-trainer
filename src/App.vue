<script setup lang="ts">

import { ref } from 'vue'
const svarighet = 5
let score = 0
const tal1 = ref([])
const tal = ref([
  {
    id: "0",
    faktor1: 9,
    faktor2: 8,
    summa: 72,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "1",
    faktor1: 6,
    faktor2: 9,
    summa: 54,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "2",
    faktor1: 7,
    faktor2: 6,
    summa: 42,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "3",
    faktor1: 8,
    faktor2: 7,
    summa: 56,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "4",
    faktor1: 7,
    faktor2: 7,
    summa: 49,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "5",
    faktor1: 5,
    faktor2: 7,
    summa: 35,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  {
    id: "6",
    faktor1: 8,
    faktor2: 8,
    summa: 64,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  },
  // {
  //   id: "7",
  //   faktor1: 6,
  //   faktor2: 7,
  //   summa: 42,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "8",
  //   faktor1: 7,
  //   faktor2: 8,
  //   summa: 56,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "9",
  //   faktor1: 9,
  //   faktor2: 9,
  //   summa: 81,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "10",
  //   faktor1: 7,
  //   faktor2: 9,
  //   summa: 63,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "11",
  //   faktor1: 6,
  //   faktor2: 6,
  //   summa: 36,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "12",
  //   faktor1: 9,
  //   faktor2: 5,
  //   summa: 45,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "13",
  //   faktor1: 7,
  //   faktor2: 5,
  //   summa: 35,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "14",
  //   faktor1: 8,
  //   faktor2: 6,
  //   summa: 48,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "15",
  //   faktor1: 9,
  //   faktor2: 7,
  //   summa: 63,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "16",
  //   faktor1: 5,
  //   faktor2: 8,
  //   summa: 40,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "17",
  //   faktor1: 9,
  //   faktor2: 6,
  //   summa: 54,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "18",
  //   faktor1: 8,
  //   faktor2: 4,
  //   summa: 32,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },
  // {
  //   id: "19",
  //   faktor1: 8,
  //   faktor2: 9,
  //   summa: 72,
  //   svar: null,
  //   isCorrect: null,
  //   isCorrected: null,
  // },

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
  this.nyFaktor1 = Math.ceil(Math.random() * this.svarighet),
    this.nyFaktor2 = Math.ceil(Math.random() * 10),
    nextTalId = nextTalId++,
    nextTalIdString = nextTalId.toString();
  tal.value.push({
    id: nextTalIdString,
    faktor1: this.nyFaktor1,
    faktor2: this.nyFaktor2,
    summa: this.nyFaktor1 * this.nyFaktor2,
    svar: null,
    isCorrect: false,
    isCorrected: false,
  })
  console.log(nextTalIdString),
    document.getElementById(nextTalIdString)!.focus();
}

</script>

<template>
  <div class="header">
    <h1>Multiplikationstränaren</h1>
    <span>{{ score }} </span><input type="number" class="svarighet" placeholder="svårighetsgrad" v-model="svarighet" />

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

      <button class="secondary" v-if="item.isCorrected == null"
        @click="item.isCorrect ? (item.isCorrected = true, focusNext()) : null">Rätta</button>

      <span v-if="item.isCorrected">Rätt!</span>
    </div>
    <div class="card"> <button id="next-button" @click="addNewTal()">Nytt tal</button>
     <button class = secondary id="refresh-button" @click="reload()">Börja om</button></div>

  </div>


</template>
