<template>
  <div class="container">
    <div>
      
    </div>
    <h1 class="title">Регистрация клиента</h1> 
    <div class="wrap">
      <div v-show="step === 1">
        
      <div class="subtext">Поля, отмеченные <span>*</span>, обязательны для заполнения</div>
      <form class="form" @submit="registerUser" novalidate onsubmit="return false;">
        <!-- Personal data -->
        <h2 class="form__title">Персональные данные</h2>
        <div class="form__divider"></div>
        <div class="form__personal">
          <div class="form__name">
            <div class="form__wrapper form-group"  >
              <label for="surname">Фамилия<span>*</span></label>
              <input class="input" @blur="$v.formItems.surname.$touch()"
              :class="{ 'form-group--error item__error': $v.formItems.surname.$error }"
              type="text" name="surname" id="surname"
              v-model.trim="$v.formItems.surname.$model"
              placeholder="Иванов"
              />
              <div v-if="$v.formItems.surname.$error" class="error">
                Поле обязательно для заполнения
              </div>
               
            </div>
              <div class="form__wrapper__left" :class="{ 'form-group--error': $v.formItems.name.$error }">
                <label for="name">Имя<span>*</span></label>
                <input class="input" @blur="$v.formItems.name.$touch()"
                v-model="formItems.name"
                type="text" name="name" id="name" placeholder="Иван">
                <div v-if="$v.formItems.name.$error" class="error">
                Поле обязательно для заполнения
                </div>
              </div>
              
          </div>
          <div class="form__wrapper">
            <label for="second_name">Отчество</label>
            <input class="input"
            v-model="formItems.second_name"
            type="text" name="second_name" id="second_name" placeholder="Иванович">
          </div>

          <div class="form__date">
            <div class="form__wrapper" :class="{ 'form-group--error': $v.formItems.name.$error }">
              <label for="date_birth">Дата рождения<span>*</span></label>
              <input class="input" @blur="$v.formItems.date_birth.$touch()"
              v-model="formItems.date_birth"
              type="date" name="date_birth" id="date_birth">
              <div v-if="$v.formItems.date_birth.$error" class="error">
                Поле обязательно для заполнения
              </div>
            </div>
            <div class="form__wrapper__left">
              <div class="form__gender__text">
                <label for="form__gender">Пол</label>
              </div>
              <div class="form__gender">
                <div class="form__gender_check">
                  <input class="form__gender_check_input" type="radio" value="male" name="exampleRadios" id="male" v-model="formItems.gender" >
                  <label for="male">
                    Мужчина
                  </label>
                </div>
                <div class="form__gender_check">
                  <input class="form__check_input" type="radio" value="female" name="exampleRadios" id="female" v-model="formItems.gender">
                  <label for="female">
                    Женщина
                  </label>
                </div>
            </div>
          </div>
          </div>

          <div class="form__wrapper" 
          :class="{ 'form-group--error': $v.formItems.group.$error }">
            <label for="group">Группа клиентов<span>*</span></label>
            <select class="select" name="group" id="group" @blur="$v.formItems.group.$touch()" v-model="formItems.group">  
              <option
              v-for="(group, index) in formItems.groups"
              :key="index" 
              >{{ group.label }}</option>
            </select>
            <div v-if="$v.formItems.group.$error" class="error">
              Поле обязательно для заполнения
            </div>
          </div>

          <div class="form__wrapper">
            <label for="doctor">Лечащий врач</label>
            <select class="select" name="doctor" id="doctor" v-model="formItems.doctor">
              <option
              v-for="(doctor, index) in formItems.doctors"
              :key="index" 
              >{{ doctor.label }}</option>
            </select >
          </div>
          
          <div class="form__check">
            <div class="form__wrapper">
              <label for="phone">Номер телефона<span>*</span></label>
              <input class="input" 
              @blur="$v.formItems.phone.$touch()"
              v-model="formItems.phone"
              v-phone
              placeholder="7(000) 000-0000"
              type="tel" name="phone" id="phone">
               <div v-if="$v.formItems.phone.$error" class="error">
                  Поле обязательно для заполнения
              </div>
            </div>
            <div class="form__wrapper__left">
              <input class="input" type="checkbox" name="sms" id="sms" v-model="formItems.sms">
              
              <div class="form__check__text">
                Не отправлять СМС
              </div>
            </div>
          </div>
        </div>

        <!-- Address -->
        <h2 class="form__title">Адрес</h2>
        <div class="form__divider"></div>

        <div class="form__address">
          <div class="form__row">
            <div class="form__wrapper">
              <label for="index">Индекс</label>
              <input class="input" type="text" name="index" id="index" v-model="formItems.index"
              placeholder="000000">
            </div>
            <div class="form__wrapper__left">
              <label for="country">Страна</label>
              <input class="input" type="text" name="country" id="country" v-model="formItems.country">
            </div>
          </div>

          <div class="form__row">
            <div class="form__wrapper">
              <label for="region">Область</label>
              <input class="input" type="text" name="region" id="region" v-model="formItems.region">
            </div>
            <div class="form__wrapper__left">
              <label for="town">Город<span>*</span></label>
              <input class="input" @blur="$v.formItems.town.$touch()" type="text" name="town" id="town" v-model="formItems.town">
              <div v-if="$v.formItems.town.$error" class="error">
                Поле обязательно для заполнения
              </div>
            </div>
          </div>

          <div class="form__row">
            <div class="form__wrapper">
              <label for="street">Улица</label>
              <input class="input" type="text" name="street" id="street" v-model="formItems.street">
            </div>
            <div class="form__wrapper__left">
              <label for="house">Дом</label>
              <input class="input" type="text" name="house" id="house" v-model="formItems.house">
            </div>
          </div>
        </div>

        <!-- Documents -->
        <h2 class="form__title">Документы</h2>
        <div class="form__divider"></div>

        <div class="form__documents">
          <div class="form__wrapper">
            <label for="type">Тип документа<span>*</span></label>
            <select class="select" @blur="$v.formItems.type.$touch()"
            name="type" id="type" v-model="formItems.type">
              <option
              v-for="(type, index) in formItems.types"
              :key="index" 
              >{{ type.label }}</option>
            </select >
            <div v-if="$v.formItems.type.$error" class="error">
              Поле обязательно для заполнения
            </div>
          </div>

          <div class="form__row">
            <div class="form__wrapper">
              <label for="series">Серия</label>
              <input class="input" type="text" name="series" id="series" v-model="formItems.series">
            </div>
            <div class="form__wrapper__left">
              <label for="number">Номер</label>
              <input class="input" type="text" name="number" id="number" v-model="formItems.number">
            </div>
          </div>

          <div class="form__wrapper">
            <label for="issued">Кем выдан</label>
            <input class="input" type="text" name="issued" id="issued" v-model="formItems.issued">
          </div>
          
          <div class="form__wrapper">
            <label for="date_issue">Дата выдачи<span>*</span></label>
            <input class="input" @blur="$v.formItems.date_issue.$touch()" type="date" name="date_issue" id="date_issue" v-model="formItems.date_issue">
            <div v-if="$v.formItems.date_issue.$error" class="error">
              Поле обязательно для заполнения
            </div>
          </div>
        </div>
        
        <button  type="submit" class="form__submit">Зарегистрировать</button>
      
    </form>
    </div>
    <div v-show="step === 2">
      <div class="completed">
        <h2>Регистрация прошла успешно!</h2>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      step: 1,
      formItems:{
        surname: '',
        name: '',
        second_name: '',
        date_birth: '',
        gender: 'male',
        group: '',
        groups: [
          {
            label: 'VIP',
            value: 'VIP'
          },
          {
            label: 'Проблемные',
            value: 'Problem'
          },
          {
            label: 'ОМС',
            value: 'OMS'
          }
        ],
        doctor: '',
        doctors: [
          {
            label: 'Иванов',
            value: 'Ivanov'
          },
          {
            label: 'Захаров',
            value: 'Zakharov'
          },
          {
            label: 'Чернышева',
            value: 'Chernisheva'
          }

        ],
        phone: '',
        sms:'',
        index: '',
        country: '',
        region: '',
        town: '',
        street: '',
        house: '',
        type: '',
        types: [
          {
            label: 'Паспорт',
            value: 'Passport'
          },
          {
            label: 'Свидетельство о рождении',
            value: 'certificate'
          },
          {
            label: 'Вод. удостоверение',
            value: 'Chernisheva'
          }

        ],
        series: '',
        number: '',
        issued: '',
        date_issue: ''
      }
    }
  },
  methods: {
    registerUser(){
      this.$v.formItems.$touch()
      if (!this.$v.formItems.$error){
      this.step++;
      }
    }
  },
  validations: {
    formItems: {
      surname: {
        required
      },
      name: {
        required
      },
      date_birth: {
        required
      },
      group: {
        required
      },
      phone: {
        required
      },
      town: {
        required
      },
      type: {
        required
      },
      date_issue: {
        required
      } 
    }
  }
}
</script>

<style lang="scss">
@import 'components/style.sass'


</style>
