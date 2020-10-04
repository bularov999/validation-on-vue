<template>
    <div>
        <div class="form-attr">
            <div>
                <h3>Атрибуты формы</h3>
            </div>
            <div class="form-row">
                <label for="surname">Фамилия</label>
                <input id="surname" type="text" v-model="surname" @blur="$v.surname.$touch()">
                <validation-error text="Введите фамилию" v-if="!$v.surname.required"></validation-error>
            </div>
            <div class="form-row">
                <label for="name">Имя</label>
                <input id="name" type="text" v-model="name">
                <validation-error text="Введите Имя" v-if="!$v.name.required"></validation-error>
            </div>
            <div class="form-row">
                <label for="lastname">Отчество</label>
                <input id="lastname" type="text">
            </div>
            <div class="form-row">
                <label for="date-of-birth">Дата рождения</label>
                <input id="date-of-birth" type="date">
            </div>
            <div class="form-row">
                <label for="number">Номер телефона</label>
                <input id="number" type="tel" v-model="number" @blur="$v.number.$touch()">
                <validation-error text="Введите число от 6 до 11 символов"
                                  v-if="!$v.number.required || !$v.number.minLength || !$v.number.maxLength" ></validation-error>
            </div>
            <div class="form-row">
                <label for="gender">Пол</label>
                <input id="gender" type="text">
            </div>
            <div class="form-row">
                <label for="clientGroup">Группа клиентов (зажмите на ctrl, чтобы выбрать несколько вариантов)</label>
                <select id="clientGroup" multiple size="3" v-model="clientGroup">
                    <option value="VIP">VIP</option>
                    <option value="Проблемные">Проблемные</option>
                    <option value="ОМС">ОМС</option>
                </select>
                <validation-error text="Выберите один или несколько вариантов"
                                  v-if="!$v.clientGroup.required"></validation-error>
            </div>
            <div class="form-row">
                <label for="doctor">Лечащий врач</label>
                <select id="doctor" size="1" v-model="doctor">
                    <option disabled>Выберите врача</option>
                    <option value="vip">Иванов</option>
                    <option value="problem">Захаров</option>
                    <option value="oms">Чернышева</option>
                </select>
            </div>
            <div class="form-row">
                <label class="label-msg" for="msg">Не отправлять смс</label>
                <input class="msg" id="msg" type="checkbox">
            </div>
        </div>
        <div>
            <button @click.prevent="$emit('change-form-attr')" class="btn" :disabled="$v.$invalid">Далее</button>
        </div>
    </div>

</template>

<script>
    import {required, minLength, maxLength} from 'vuelidate/lib/validators'
    import validationError from "./validateTypes/validationError";

    export default {
        name: "formsAttr.vue",
        data() {
            return {
                surname: "",
                name: "",
                number: "",
                clientGroup: [],
                doctor: ''
            }
        },
        components: {
            'validation-error': validationError
        },
        validations: {
            surname: {
                required
            },
            name: {
                required,
            },
            number: {
                required,
                minLength: minLength(6),
                maxLength: maxLength(11)
            },
            clientGroup: {
                required: function (client) {
                    if (client.length < 1) {
                        return false
                    }
                    return true
                }
            }
        }
    }
</script>

<style lang="sass" scoped>

    .form-attr
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

            .label-msg
                flex: 1

            .msg
                flex: 0.3
                height: 30px
                margin-right: 60%
    .btn
        background: forestgreen
        color: #fff
        border: none
        padding: 15px
        border-radius: 10%
        margin-top: 30px
</style>