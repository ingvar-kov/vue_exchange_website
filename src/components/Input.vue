<script>
    export default {
        props: {
            changeAmount: {
                type: Function,
                required: true
            },
            convert: {
                type: Function,
                required: true
            },
        }
    }
</script>

<template>
    <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Введите число">
    <button @click="convert()">Конвертировать</button>
</template>

<style scoped>
    input, button {
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
    }
    button {
        background-color: rgb(217, 176, 255);
        cursor: pointer;
        transition: 600ms;
    }
    button:hover {
        background-color: rgb(197, 135, 255);
    }
</style>
