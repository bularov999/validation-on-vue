<template>
    <div class="passport">
        <div><h3>Паспорт</h3></div>
        <div class="form-row">
            <label for="doc">Тип документа</label>
            <select id="doc" size="1" v-model="doc">
                <option disabled>Выберите тип</option>
                <option value="passport">Паспорт</option>
                <option value="cof">Свидетельство о рождении</option>
                <option value="license"> Вод. удостоверение</option>
            </select>
            <validation-error text="Выберите тип" v-if="!$v.doc.required"></validation-error>
        </div>
        <div class="form-row">
            <label for="passport-series">Серия</label>
            <input id="passport-series" type="tel">
        </div>
        <div class="form-row">
            <label for="passport-number">Номер</label>
            <input id="passport-number" type="text">
        </div>
        <div class="form-row">
            <label for="issued-by">Кем выдан</label>
            <input id="issued-by" type="text">
        </div>
        <div class="form-row">
            <label for="date-of-issue">Дата выдачи</label>
            <input id="date-of-issue" type="date" v-model="date">
            <validation-error text="Задайте корректную дату" v-if="!date"></validation-error>
        </div>
        <div class="form-row">
            <button class="btn" :disabled="false" @click="createUser">Создать</button>
        </div>


    </div>
</template>

<script>
    import validationError from "./validateTypes/validationError";
    import {required} from 'vuelidate/lib/validators'


    export default {
        name: "passport.vue",
        components: {
            'validation-error': validationError
        },
        data() {
            return {
                doc: '',
                date: ''
            }
        },
        methods: {
          createUser () {
              alert('Клиент успешно создан')

          }
        },
        validations : {
            doc: {
                required
            },
            date: {
                required
            }
        }
    }
</script>

<style lang="sass" scoped>
    .passport
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