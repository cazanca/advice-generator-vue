<script setup>
    import { ref, onBeforeMount } from 'vue'
import axios from 'axios'

    let adviceNumber = ref('117')
    let advice = ref("It is easy to sit up and take notice, what's difficult is getting up and taking action.")

const getAdvice = async () => {
    try {
        const {data} = await axios.get('https://api.adviceslip.com/advice')
        console.log(data.slip.advice)
        adviceNumber.value = data.slip.id
        advice.value = data.slip.advice
    } catch (error) {
        console.error(error)
    }
}    

onBeforeMount(() => getAdvice())
</script>

<template>
    <article class="card">
        <h1 class="title">advice #{{adviceNumber}}</h1>
        <p class="advice">
            "{{advice}}"
        </p>
        
        <div class="divider">
            <img src="../assets/images/pattern-divider-mobile.svg" alt="Divider">
        </div>
        <div class="dice-container">
            <img src="../assets/images/icon-dice.svg" alt="Dice">
        </div>
    </article>
</template>