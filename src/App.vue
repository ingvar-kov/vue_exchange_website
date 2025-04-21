<script setup>
    import { ref } from 'vue'
    import Input from './components/Input.vue'
    import Selector from './components/Selector.vue'

    const amount = ref(0)
    const cryptoFirst = ref('')
    const cryptoSecond = ref('')
    const error = ref('')

    const changeAmount = (value) => {
        amount.value = value
        error.value = '' // Сбрасываем ошибку при изменении суммы
    }

    const setCryptoFirst = (value) => {
        cryptoFirst.value = value
    }

    const setCryptoSecond = (value) => {
        cryptoSecond.value = value
    } // <- Точка с запятой вместо запятой

    const convert = () => { // Правильное объявление функции
        if (amount.value <= 0) {
            error.value = 'Укажите сумму'
            return
        } else if(cryptoFirst.value == cryptoSecond.value) {
            error.value = 'Выберите другую валюту'
            return
        }
        this.error = ''
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
    <div>
        {{ cryptoFirst }}  {{ cryptoSecond }}
    </div>
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
</style>