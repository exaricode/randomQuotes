<template>
    <div class="flex flex-col justify-center items-center
        border-2 border-black border-solid rounded-md">
        <div class="py-2 px-2 mx-auto mt-2 text-xl">
            <slot name="quote"></slot>
        </div>
        <div class="p-2 mb-2 self-end mr-4 text-lg">
            <slot name="author"></slot>
        </div>
        <div v-if="clickBtn"
            class="self-end p-2 mr-4">
            <next-quote-btn @click="emits('clicked')">{{ btnText }}</next-quote-btn>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, watchEffect } from 'vue';
import NextQuoteBtn from './NextQuoteBtn.vue';

const clickBtn = ref(true);

const emits = defineEmits([
    'clicked'
]);

const btnText = ref('next quote');

onMounted(() => {
    if (!clickBtn.value) {
        watchEffect(() => {
            intervalQoutes();
        })
    }
})

function intervalQoutes(){
    setInterval(() => emits('clicked'), 5000);
}

</script>

<style scoped>

</style>