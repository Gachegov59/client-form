<template>
    <div class="container">
        <h1>Форма</h1>
        <div class="blocks">
            <div class="blocks__item _50">
                <form class="form">

                    <div class="form__item ">
                        <label class="form__label" for="firstName">Фамилия
                            <span class="form__item-required"
                                  v-if="!this.$v.firstName.required || this.$v.firstName.$invalid">*</span>
                        </label>
                        <div class="form__input"
                             :class="{'_isInvalid': $v.firstName.$error, '_isValid': !$v.firstName.$invalid}">
                            <input id="firstName"
                                   type="text"
                                   v-model.trim="$v.firstName.$model">
                            <div class="form__item-feedback">
                                <span v-if="!this.$v.firstName.minLength">Минимум {{$v.firstName.$params.minLength.min}} буквы</span>
                                <span v-if="!this.$v.firstName.maxLength">Максимум  {{$v.firstName.$params.maxLength.max}} буквы</span>
                            </div>
                        </div>


                    </div>
                    <div class="form__item ">
                        <label class="form__label" for="lastName">Имя
                            <span class="form__item-required"
                                  v-if="!this.$v.lastName.required || this.$v.lastName.$invalid">*</span>
                        </label>
                        <div class="form__input"
                             :class="{'_isInvalid': $v.lastName.$error, '_isValid': !$v.lastName.$invalid}">
                            <input id="lastName"
                                   type="text"
                                   v-model.trim="$v.lastName.$model">
                            <div class="form__item-feedback">
                                <span v-if="!this.$v.lastName.minLength">Минимум {{$v.lastName.$params.minLength.min}} буквы</span>
                                <span v-if="!this.$v.lastName.maxLength">Максимум  {{$v.lastName.$params.maxLength.max}} буквы</span>
                            </div>
                        </div>


                    </div>
                    <div class="form__item ">
                        <label class="form__label" for="age">Возраст
                            <span class="form__item-required"
                                  v-if="!this.$v.age.required || this.$v.age.$invalid">*</span>
                        </label>
                        <div class="form__input" :class="{'_isInvalid': $v.age.$error, '_isValid': !$v.age.$invalid}">
                            <input id="age"
                                   type="number"
                                   v-model.trim="$v.age.$model">
                            <div class="form__item-feedback">
                                <span v-if="!this.$v.age.between">Между  {{$v.age.$params.between.min}} и  {{$v.age.$params.between.max}} </span>
                            </div>
                        </div>


                    </div>
                    <div class="form__btn">
                        <button class="btn _border _r6">Отправить</button>
                    </div>
                </form>
            </div>
            <div class="blocks__item _30">
                <pre style="margin-top:0">{{ $v }}</pre>
                {{showV()}}
            </div>
        </div>
    </div>
</template>

<script>
    import {required, minLength, maxLength, between} from 'vuelidate/lib/validators'

    export default {
        name: "form",
        data() {
            return {
                firstName: '',
                lastName: '',
                age: 0,
            }
        },
        validations: {
            firstName: {
                required,
                minLength: minLength(3),
                maxLength: maxLength(10)
            },
            lastName: {
                required,
                minLength: minLength(5),
                maxLength: maxLength(12)
            },
            age: {
                required,
                between: between(15, 40)
            }
        },
        methods: {
            showV() {
                // console.log(this.$v.firstName.minLength)
                console.log(this.$v.age.required )
                console.log(!this.$v.age.$invalid)
            }
        }
        // methods: {
        //     status(validation) {
        //         return {
        //             error: validation.$error,
        //             dirty: validation.$dirty
        //         }
        //     }
        // }
    }
</script>

<style scoped>

</style>