<template>
    <div>
        <div class="address">
            <div><h3>Адресс</h3></div>
            <div class="form-row">
                <label for="index">Индекс</label>
                <input id="index" type="text">
            </div>
            <div class="form-row">
                <label for="country">Страна</label>
                <input id="country" type="text">
            </div>
            <div class="form-row">
                <label for="region">Область</label>
                <input id="region" type="text">
            </div>
            <div class="form-row">
                <label for="city">Город</label>
                <input id="city" type="text" v-model="city" @blur="$v.city.$touch()">
                <validation-error text="Введите свой город" v-if="$v.city.$invalid"></validation-error>
            </div>
            <div class="form-row">
                <label for="street">Улица</label>
                <input id="street" type="text">
            </div>
            <div class="form-row">
                <label for="house">Дом</label>
                <input id="house" type="text">
            </div>
        </div>
        <div>
            <button
              :disabled="$v.$invalid"
              @click.prevent="$emit('change-form-attr')"
              class="btn"
            >
                Далее
            </button>
        </div>
    </div>
</template>

<script>
    import validationError from "./validateTypes/validationError";
    import {required} from 'vuelidate/lib/validators'

    export default {
        name: "userAddress.vue",
        components: {
            'validation-error': validationError
        },
        data() {
            return {
                city: ''
            }
        },
        validations: {
            city: {
                required
            }
        }
    }
</script>

<style lang="sass" scoped>
    .address
        display: flex
        flex-direction: column

        .form-row
            display: flex
            justify-content: flex-end
            padding: .5em
            position: relative


            label
                padding: .5em 1em .5em 0
                flex: 1

            input
                flex: 2
                padding: .5em

            select
                flex: 2
                padding: .5em

    .btn
      background: forestgreen
      color: #fff
      border: none
      padding: 15px
      border-radius: 10%
      margin-top: 30px
</style>