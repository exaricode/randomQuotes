<template>
    <div class="w-full h-full flex justify-center items-center content-center"
        :class="bgColor">
        <quotes-display-vue @clicked="randomQuote" class="max-w-xl w-1/2 h-1/4 max-h-60">
            <template v-slot:quote>{{ quote }}</template>
            <template v-slot:author>{{ author }}</template>
        </quotes-display-vue>
    </div>
</template>

<script setup>
import QuotesDisplayVue from './QuotesDisplay.vue';

import { ref, onMounted } from 'vue';
import axios from 'axios';


const quotes = ref();
const response = ref();
const len = ref(0);

const quote = ref();
const author = ref();
const bgColor = ref();

const colorArr = ref([
    'bg-gradient-to-b from-cyan-500 to-cyan-300', 
    'bg-gradient-to-b from-red-500 to-red-300',
    'bg-gradient-to-b from-green-500 to-green-300',
    'bg-gradient-to-b from-purple-500 to-purple-300',
    'bg-gradient-to-b from-orange-500 to-orange-300',
    'bg-gradient-to-b from-amber-500 to-amber-300',
    'bg-gradient-to-b from-yellow-500 to-yellow-300',
    'bg-gradient-to-b from-lime-500 to-lime-300',
    'bg-gradient-to-b from-emerald-500 to-emerald-300',
    'bg-gradient-to-b from-teal-500 to-teal-300',
    'bg-gradient-to-b from-sky-500 to-sky-300',
    'bg-gradient-to-b from-blue-500 to-blue-300',
    'bg-gradient-to-b from-indigo-500 to-indigo-300',
    'bg-gradient-to-b from-violet-500 to-violet-300',
    'bg-gradient-to-b from-fuchsia-500 to-fuchsia-300',
    'bg-gradient-to-b from-pink-500 to-pink-300',
    'bg-gradient-to-b from-rose-500 to-rose-300'
])

onMounted(async () => {
    // get quotes from quotes.json
    response.value = await axios.get('/src/assets/quotes.json');
    quotes.value = response.value.data.quotes;
    len.value = quotes.value.length;
    randomQuote();
});


// get random quote
function randomQuote(){
    let x = randomizer();
    quote.value = quotes.value[x].quote;
    author.value = quotes.value[x].author;
    randomBgColor();
}

// get random background color
function randomBgColor(){
    let x = colorArr.value.length;
    bgColor.value = colorArr.value[randomizer(x)];
    console.log(bgColor.value);
}

// random number function
function randomizer(l = len.value) {
    return Math.floor(Math.random() * l);
}

</script>

<style scoped>

</style>