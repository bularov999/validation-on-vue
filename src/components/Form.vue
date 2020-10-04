<template>
    <div class="container">
        <form>
            <form-attr v-if="userAddress" v-on:change-form-attr="changeSlide"/>
            <user-address v-else-if="formAttr" v-on:change-form-attr="changeSlide" />
            <passport v-else-if="passport"/>
        </form>
    </div>
</template>

<script>
    import UserAddress from "./forms/UserAddress";
    import FormsAttr from "./forms/FormsAttr";
    import Passport from "./forms/Passport";


    export default {
        name: "form.vue",
        components: {
            'user-address': UserAddress,
            'form-attr': FormsAttr,
            'passport': Passport
        },
        data() {
            return {
                sides: 0,
                userAddress: true,
                formAttr: false,
                passport: false
            }
        },
        methods: {
            changeSlide() {
                this.sides++
                if (this.sides === 1) {
                    this.userAddress = false
                    this.formAttr = true
                }
                else if (this.sides === 2) {
                    this.formAttr = false
                    this.passport = true
                }
            }
        }
    }
</script>

<style lang="sass" scoped>
    .container
        width: 70%
        margin: 0 auto
        display: flex
        flex-direction: column
        background-color: whitesmoke
        padding: 30px
        border-radius: 3px

    form
        width: 100%
</style>