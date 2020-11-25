<template>
    <div class="container">
        <div class="blocks">
            <div class="blocks__item ">
                <form class="form" @submit.prevent="submitForm" v-if="!isAdded">
                    <h1>Клиентская форма</h1>
                    <div class="form__sections">
                        <section class="form__section">
                            <h2> ФИО</h2>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="firstName">Фамилия
                                        <span class="form__item-required">*</span>
                                    </label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.firstName.$error, '_isValid': !$v.form.firstName.$invalid   }">
                                        <!--                             :class="$v.form.firstName.$error  ? '_isInvalid' : ''">-->
                                        <input class="form__input" id="firstName" type="text"
                                               v-model.trim="$v.form.firstName.$model"
                                               tabindex="1">
                                        <div class="form__item-feedback">
                                            <span v-if="$v.form.firstName.$dirty && !$v.form.firstName.minLength ">От {{$v.form.firstName.$params.minLength.min}} букв</span>
                                            <span v-if="$v.form.firstName.$dirty && !$v.form.firstName.required">Обязательное поле</span>
                                            <!--                                <span v-if="!$v.form.firstName.maxLength">Не более  {{$v.form.firstName.$params.maxLength.max}} букв</span>-->
                                            <!--                                <span v-if="$v.form.firstName.minLength && $v.form.firstName.maxLength && !$v.form.firstName.alpha">Только буквы</span>-->
                                        </div>
                                    </div>


                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="lastName">Имя
                                        <span class="form__item-required">*</span>
                                    </label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.lastName.$error, '_isValid': !$v.form.lastName.$invalid}">
                                        <input class="form__input" id="lastName"
                                               type="text"
                                               v-model.trim="$v.form.lastName.$model"
                                               tabindex="2">
                                        <div class="form__item-feedback">
                                            <span v-if="!$v.form.lastName.minLength">От {{$v.form.lastName.$params.minLength.min}} буквы</span>
                                            <span v-if="$v.form.lastName.$dirty && !$v.form.lastName.required">Обязательное поле</span>
                                            <span v-if="!$v.form.lastName.maxLength && $v.form.lastName.$dirty">не более  {{$v.form.lastName.$params.maxLength.max}} буквы</span>
<!--                                            <span v-if="$v.form.lastName.minLength && $v.form.lastName.maxLength && !$v.form.lastName.alpha && $v.form.lastName.$dirty">Только буквы</span>-->
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="patronymic">Отчество</label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.patronymic.$error, '_isValid': $v.form.patronymic.$model}">
                                        <input class="form__input" id="patronymic" type="text"
                                               v-model.trim="$v.form.patronymic.$model"
                                               tabindex="3">
                                        <div class="form__item-feedback">
                                            <span v-if="!$v.form.patronymic.minLength">От {{$v.form.patronymic.$params.minLength.min}} буквы</span>
                                            <span v-if="!$v.form.patronymic.maxLength">не более  {{$v.form.patronymic.$params.maxLength.max}} буквы</span>
                                            <span v-if="$v.form.patronymic.minLength && $v.form.patronymic.maxLength && !$v.form.patronymic.alpha">Только буквы</span>
                                        </div>
                                    </div>
                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="birthDate">Дата рождения
                                        <span class="form__item-required">*</span>
                                    </label>
                                    <div class="form__group _no-after"
                                         :class="{'_isInvalid': $v.form.birthDate.$error, '_isValid': $v.form.birthDate.$model}">
                                        <input class="form__input" id="birthDate"
                                               type="date"
                                               tabindex="4"
                                               v-model="$v.form.birthDate.$model"
                                        >
                                        <div class="form__item-feedback">
                                            <span v-if="$v.form.birthDate.$dirty && !$v.form.birthDate.required">Обязательное поле</span>
                                        </div>
                                    </div>


                                </div>
                            </div>


                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="phone">Номер телефона</label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.phone.$error, '_isValid': $v.form.phone.$model}">
                                        <input class="form__input" id="phone"
                                               type="tel"
                                               v-model="$v.form.phone.$model"
                                               tabindex="5"
                                               name="phone"
                                               maxlength="11">
                                        <div class="form__item-feedback">
                                            <span v-if="$v.form.phone.$dirty && !$v.form.phone.required">Обязательное поле</span>
                                        </div>
                                    </div>
                                </div>
                                <div class="form__items">
                                    <div class="form__items-name">Пол</div>
                                    <div class="form__block">
                                        <div class="form__item">
                                            <label class="form__label _small" for="male">мужской </label>
                                            <div class="form__group">
                                                <input class="form__input" id="male"
                                                       type="radio"
                                                       name="gender"
                                                       value="male"
                                                       v-model="form.gender"
                                                       tabindex="6">
                                            </div>
                                        </div>
                                        <div class="form__item ">
                                            <label class="form__label _small" for="female">женский </label>
                                            <div class="form__group">
                                                <input class="form__input" id="female"
                                                       type="radio"
                                                       name="gender"
                                                       value="female"
                                                       tabindex="7"
                                                       v-model="form.gender">
                                            </div>


                                        </div>
                                    </div>
                                </div>
                            </div>

                            <div class="form__item">
                                <label class="form__label" for="lastName">Группа клиентов
                                    <span class="form__item-required">*</span>
                                </label>
                                <div class="form__group _no-after"
                                     :class="{'_isInvalid': $v.form.group.$error, '_isValid': $v.form.group.$model}">
                                    <select class="form__select scroll" multiple v-model="$v.form.group.$model">
                                        <option value="VIP">VIP</option>
                                        <option value="Проблемные">Проблемные</option>
                                        <option value="ОМС">ОМС</option>
                                    </select>
                                    <div class="form__item-feedback">
                                        <span v-if="$v.form.group.$dirty && !$v.form.group.required">Обязательное поле</span>
                                    </div>
                                </div>
                            </div>
                            <div class="form__item">
                                <label class="form__label" for="lastName">Лечащий врач. </label>
                                <div class="form__group">
                                    <select class="form__select scroll" v-model="form.doctor">
                                        <option value="Иванов">Иванов</option>
                                        <option value="Захаров">Захаров</option>
                                        <option value="Чернышева">Чернышева</option>
                                    </select>

                                </div>
                            </div>
                            <div class="form__item _checkbox">
                                <input class="form__input" id="message"
                                       type="checkbox"
                                       name="gender"
                                       v-model="form.message">
                                <label class="form__label _radio" for="message">Не отправлять смс </label>
                            </div>
                        </section>

                        <section class="form__section">
                            <h2> Адресс</h2>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="index">Индекс</label>
                                    <div class="form__group ">
                                        <input class="form__input" id="index" type="number"
                                               v-model.number="form.index">
                                    </div>
                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="country">Странна</label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.country.$error, '_isValid': $v.form.country.$model}">
                                        <input class="form__input" id="country" type="text" v-model="form.country"
                                               v-model.trim="form.country">
                                    </div>
                                </div>

                            </div>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="region">Область</label>
                                    <div class="form__group">
                                        <input class="form__input" id="region" type="text" v-model="form.region">
                                    </div>
                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="city">Город
                                        <span class="form__item-required">*</span>
                                    </label>
                                    <div class="form__group"
                                         :class="{'_isInvalid': $v.form.city.$error, '_isValid': $v.form.city.$model}">
                                        <input class="form__input"
                                               id="city"
                                               type="text"
                                               v-model="$v.form.city.$model">
                                        <div class="form__item-feedback">
                                            <span v-if="$v.form.city.$dirty && !$v.form.city.required">Обязательное поле</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="street">Улица</label>
                                    <div class="form__group">
                                        <input class="form__input" id="street" type="text" v-model="form.street">
                                    </div>
                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="house">Дом</label>
                                    <div class="form__group">
                                        <input class="form__input" id="house" type="text" v-model="form.house">
                                    </div>
                                </div>
                            </div>
                        </section>

                        <section class="form__section">
                            <h2> Документ</h2>
                            <div class="form__item">
                                <label class="form__label" for="lastName">Тип документа
                                    <span class="form__item-required">*</span>
                                </label>
                                <div class="form__group _no-after"
                                     :class="{'_isInvalid': $v.form.documentType.$error, '_isValid': $v.form.documentType.$model}">
                                    <select class="form__select" v-model="$v.form.documentType.$model">
                                        <option value="passport">Паспорт</option>
                                        <option value="birth-certificate">Свидетельство о рождении</option>
                                        <option value="driver's-license">Вод. удостоверение</option>
                                    </select>
                                    <div class="form__item-feedback">
                                        <span v-if="$v.form.documentType.$dirty && !$v.form.documentType.required">Обязательное поле</span>
                                    </div>

                                </div>
                            </div>
                            <div class="form__row ">
                                <div class="form__item ">
                                    <label class="form__label" for="id">Серия</label>
                                    <div class="form__group">
                                        <input class="form__input" id="id" type="text" v-model="form.documentSerial">
                                    </div>
                                </div>
                                <div class="form__item ">
                                    <label class="form__label" for="serialNumber">Номер</label>
                                    <div class="form__group">
                                        <input class="form__input" id="serialNumber" type="text"
                                               v-model="form.documentSerialNumber">
                                    </div>
                                </div>
                            </div>
                            <div class="form__item ">
                                <label class="form__label" for="from">Кем выдан</label>
                                <div class="form__group">
                                    <input class="form__input" id="from" type="text" v-model="form.getFrom">
                                </div>
                            </div>
                            <div class="form__item ">
                                <label class="form__label" for="dataGot">Дата выдачи
                                    <span class="form__item-required">*</span>
                                </label>
                                <div class="form__group _no-after"
                                     :class="{'_isInvalid': $v.form.documentDate.$error, '_isValid': $v.form.documentDate.$model}">
                                    <input class="form__input" id="dataGot" type="date"
                                           v-model="$v.form.documentDate.$model">
                                    <div class="form__item-feedback">
                                        <span v-if="$v.form.documentDate.$dirty && !$v.form.documentDate.required">Обязательное поле</span>
                                    </div>
                                </div>
                            </div>
                        </section>
                    </div>
                    <div class="form__btn">
                        <button class="btn _border _r6">Отправить</button>
                    </div>

                </form>
                <section v-else>
                    <h2> Клиент {{this.form.firstName}} {{this.form.lastName}} добавлен</h2>
                    <div class="message">
                        <span v-for="item in this.form" :key="item.i">
                                       {{item}}
                        </span>

                    </div>


                    <!--                    <pre> {{this.form}}} добавлен</pre>-->
                </section>
            </div>
            <!--            <div class="blocks__item _30">-->
            <!--                <pre class="custom-scroll" style="margin-top:0">{{ $v }}</pre>-->
            <!--                {{showV()}}-->
            <!--            </div>-->
        </div>
    </div>
</template>

<script>
    import {required, minLength, maxLength} from 'vuelidate/lib/validators'
    // import Vue from 'vue'

    // Vue.directive('phone', {
    //     bind(el) {
    //         el.oninput = function (e) {
    //             if (!e.isTrusted) {
    //                 return;
    //             }
    //
    //             // const x = this.value.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
    //             // this.value = !x[2] ? x[1] : '7' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
    //             // this.value = 7;
    //
    //         }
    //     },
    // });
    export default {

        name: "form",
        data: () => ({
            isAdded: false,
            form: {
                firstName: '',
                lastName: '',
                patronymic: '',
                birthDate: '',
                phone: '',
                gender: '',
                group: [],
                doctor: '',
                message: false,
                country: '',
                region: '',
                city: '',
                street: '',
                house: '',
                index: '',
                getFrom: '',
                documentType: '',
                documentSerial: '',
                documentSerialNumber: '',
                documentDate: ''
            },
            doctor: ['Иванов', 'Захаров', 'Чернышева'],
            clients: ['VIP', 'Проблемные', 'ОМС'],
            documentType: ['Паспорт', 'Свидетельство о рождени', 'Вод. удостоверение']
        }),
        validations: {
            form: {
                firstName: {required, minLength: minLength(3), maxLength: maxLength(15)},
                lastName: {required, minLength: minLength(3), maxLength: maxLength(15)},
                patronymic: {minLength: minLength(3), maxLength: maxLength(15)},
                birthDate: {required},
                phone: {required, minLength: minLength(11), maxLength: maxLength(11)},
                group: {required},
                country: {minLength: minLength(3), maxLength: maxLength(20)},
                region: {minLength: minLength(3), maxLength: maxLength(20)},
                city: {required},
                documentType: {required},
                documentDate: {required}
            }
        },
        methods: {
            submitForm() {

                if (!this.$v.form.$invalid) {
                    this.isAdded = true
                    console.log('хорошо')
                }
                if (this.$v.form.$invalid) {
                    this.$v.form.$touch();
                    console.log('не прошла')
                }
                // console.log(this.$v)
                // console.log(this.$v.form.firstName.$params.length)
            },
            showV() {
                // function   ()=> {
                //     setTimeout('sayHi', 1000);
                // }
                // console.log($v.form.firstName.minLength)
                // console.log($v.form.date.required)
                // console.log(!$v.form.date.$invalid)
            },
        }

    }

</script>

<style scoped>

</style>