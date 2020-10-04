<template>
    <small>*{{text}}</small>
</template>

<script>
    export default {
        name: "validationError.vue",
        props: ['text']
    }
</script>

<style lang="sass" scoped>
    small
        color: forestgreen
        font-family: "Arial"
        font-weight: bold
        font-size: 0.9rem
        position: absolute
        width: 50%

</style>