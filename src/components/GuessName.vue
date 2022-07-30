<template>
    <p>Resposta: {{ answer.name }}</p>

    <p>Opcoes:</p>
    <ul v-for="(option, index) in options" :key="index">
        <li>{{ option.name }}</li>
    </ul>
</template>

<script>
export default {
    name: 'GuessName',
    props: {
        answer: Object,
        options: Array,
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
    font-size: 30px;
    font-weight: 800;
}
</style>