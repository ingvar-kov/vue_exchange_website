<script setup>
    defineProps({
        setCrypto: {
            type: Function,
            required: true
        },
        currentCrypto: {
            type: String,
            required: false
        }
    })
</script>

<template>
  <ul>
    <li @click="setCrypto('BTC')" :class="{ active: currentCrypto === 'BTC' }">
      Bitcoin
    </li>
    <li @click="setCrypto('ETH')" :class="{ active: currentCrypto === 'ETH' }">
      ETH
    </li>
    <li @click="setCrypto('USDT')" :class="{ active: currentCrypto === 'USDT' }">
      USDT
    </li>
  </ul>
</template>

<style scoped>
    ul {
        list-style: none;
        padding: 0;
        border-radius: 3px;
        border: 3px solid black;
        width: 9vw;
    }
    li {
        display: block;
        background: rgb(56, 3, 63);
        color: white;
        padding: 1.5rem 0;
    }
    li:hover, li.active {
        background: rgb(26, 1, 29);
        cursor: pointer;
        transition: 600ms;
    }
    .active {
        font-weight: bold;
        color: #42b983;
        transition: 600ms;
    }
</style>
