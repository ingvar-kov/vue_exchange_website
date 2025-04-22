<script setup>
    import { ref } from 'vue'
    import Input from './components/Input.vue'
    import Selector from './components/Selector.vue'
    import CryptoConvert from 'crypto-convert';

    const cryptoConverter = new CryptoConvert();

    const cryptoFirst = ref('')
    const cryptoSecond = ref('')
    const amount = ref(0)
    const error = ref('')
    const res = ref(null)

    const changeAmount = (value) => {
        amount.value = value
        error.value = ''
    }

    const setCryptoFirst = (value) => {
        cryptoFirst.value = value
    }

    const setCryptoSecond = (value) => {
        cryptoSecond.value = value
    }

    const convert = async () => {
        if (cryptoFirst.value === cryptoSecond.value) {
            error.value = 'Выберите валюту'
            return
        } else if (amount.value <= 0) {
            error.value = 'Укажите сумму'
            return
        }
        
        error.value = ''
        
        await cryptoConverter.ready()
    
        res.value = cryptoConverter[cryptoFirst.value][cryptoSecond.value](amount.value)
    }
</script>


<template>
    <h1>Crypto exchange</h1>
    <Input :changeAmount="changeAmount" :convert="convert"/>
    <p v-if="error != ''" className="error">{{ error }}</p>
    <div class="selectors">
        <Selector :setCrypto="setCryptoFirst" :currentCrypto="cryptoFirst" />
        <Selector :setCrypto="setCryptoSecond" :currentCrypto="cryptoSecond" />
    </div>
    <div className="course">
        {{ cryptoFirst }}  {{ cryptoSecond }}
    </div>
    <p v-if="res !== null" className="res">{{ res }}</p>
</template>

<style scoped>
    .selectors {
    box-sizing: border-box;
    display: flex;
    justify-content: space-between;
    width: 20vw;
    margin: 0 auto;
    }
    .error {
        font-weight: bold;
        color: white;
    }
    .course {
        font-weight: bold;
        color: white;
    }
    .res {
        display: block;
        box-sizing: border-box;
        outline: none;
        margin: 0 auto;
        border: none;
        border-radius: 3px;
        padding: 1rem 1.5rem;
        font-size: 1.5rem;
        width: 20vw;
        font-weight: bold;
        margin-bottom: 1.5rem;
        background-color: #42b983;
    }
    @media (max-width: 767px) {
        .selectors, .res {
            width: 60vw;
        }
    }
</style>