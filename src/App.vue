<template>
  <div id="app">
    <h1>Форма создания клиента</h1>

    <form @submit.prevent="success" action="">
      <div class="form">

        <div class="form__left">

          <div class="form-group" >
              <label for="name">Имя</label>
              <input v-model.trim="$v.name.$model" type="text" id="name">
              <span class="error" v-if="!$v.name.required">Обязательное поле</span>    
          </div>

          <div class="form-group">
              <label for="surname">Фамилия</label>
              <input v-model.trim="$v.surname.$model" type="text" id="surname">
              <span class="error" v-if="!$v.surname.required">Обязательное поле</span>    
          </div>

          <div class="form-group">
            <label for="second-name">Отчество</label>
            <input type="text" id="second-name">
          </div>

          <div class="form-group">
            <label for="birth-date">Дата рождения</label>
            <input type="date" id="birth-date">
          </div>

          <div class="form-group phone">
              <label for="phone">Номер телефона</label>
              <input v-model.trim="$v.phone.$model" type="text" id="phone">
              <span class="error" v-if="!$v.phone.checkPhoneNumber">
                Номер должен начинаться с цифры 7, не содержать пробелов и других символов
              </span> 
          </div>

          <div class="form-group">
            Пол:
            <div class="gender">
              <label for="female">Женский</label>
              <input type="radio" checked id="female" name="gender">
              <label for="male">Мужской</label>
              <input type="radio" id="male" name="gender">
            </div>
          </div>

          <div 
            class="clients-group form-group" 
          >
            <label for="clients-group">Группа клиентов</label>
            <select v-model.trim="$v.clientsGroup.$model" id="clients-group" name="clients-group" multiple>
              <option value="vip">VIP</option>
              <option value="tricky">Проблемные</option>
              <option value="omi">ОМС</option>
            </select>
            <span class="error" v-if="!$v.clientsGroup.required">Обязательное поле</span>    
          </div>

          <div class="form-group">
            <label for="doctor">Лечащий врач</label>
            <select id="doctor" name="doctor">
              <option value="ivanov">Иванов</option>
              <option value="zacharov">Захаров</option>
              <option value="chernisheva">Чернышева</option>
            </select>
          </div>

          <div>
            <label for="message">Не отправлять СМС</label>
            <input type="checkbox" id="message">
          </div>

        </div>

        <div class="form__right">
          <fieldset class="address">

            <legend>Адрес</legend>
            
            <div class="form-group">
              <label for="zip-code">Индекс</label>
              <input type="text" id="zip-code">
            </div>

            <div class="form-group">
              <label for="country">Страна</label>
              <input type="text" id="country">
            </div>

            <div class="form-group">
              <label for="region">Область</label>
              <input type="text" id="region">
            </div>

            <div class="form-group">
              <label for="city">Город</label>
              <input v-model.trim="$v.city.$model" type="text" id="city">
              <span class="error" v-if="!$v.city.required">Обязательное поле</span>    
            </div>

            <div class="form-group">
              <label for="street">Улица</label>
              <input type="text" id="street">
            </div>

            <div class="form-group">
              <label for="apartments">Дом</label>
              <input type="text" id="apartments">
            </div>
          </fieldset>

          <fieldset class="documents">
            <legend>Паспорт</legend>

            <div class="docs form-group"
            >
              <label for="docs">Тип документа</label>
              <select v-model="$v.docs.$model" id="docs" name="docs">
                <option value="passport">Паспорт</option>
                <option value="birth-sertificate">Свидетельство о рождении</option>
                <option value="drivers-licence">Водительское удостоверение</option>
              </select>
              <span class="error" v-if="!$v.docs.required">Обязательное поле</span>  
            </div>

            <div class="form-group">
              <label for="series">Серия</label>
              <input type="text" id="series">
            </div>

            <div class="form-group">
              <label for="number">Номер</label>
              <input type="text" id="number">
            </div>

            <div class="form-group">
              <label for="place">Кем выдан</label>
              <input type="text" id="place">
            </div>

            <div class="form-group">
              <label for="date">Когда выдан</label>
              <input v-model.trim="$v.date.$model" type="date" id="date">
              <span class="error" v-if="!$v.date.required">Обязательное поле</span>    
            </div>

          </fieldset>
        </div>
        
      </div>

      <button 
        type="submit"
        :disabled="$v.$invalid"
      >
        Создать клиента
      </button>


    </form>

    <div style="display: none" :class="{'modal__content': isModal}">
      Новый клиент успешно создан!
    </div>

  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'

const checkPhoneNumber = (value) => /^[7]\d{10}$/.test(value)

export default {
  name: 'App',
  data() {
    return {
      name: '',
      surname: '',
      phone: '',
      city: '',
      clientsGroup: [],
      docs: '',
      date: '',
      isModal: false
    }
  },
  validations: {
    name: {
      required
    },
    surname: {
      required
    },
    phone: {
      required,
      checkPhoneNumber
    },
    city: {
      required
    },
    clientsGroup: {
      required
    },
    docs: {
      required
    },
    date: {
      required
    }
  },
  methods: {
    success() {
      this.isModal = true
      setTimeout(() => {
        this.isModal = false
      }, 1500)
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&display=swap');

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  color: inherit;
  font: inherit;
}

body {
  padding: 15px;
  height: 100vh;
}

#app {
  font-family:  'Montserrat', sans-serif;
  font-size: 14px;
  font-weight: 500;
}

h1 {
  margin: 10px auto;
  text-align: center;
  font-size: 20px;
}

label {
  margin-right: 5px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form {
  display: flex;
  gap: 10px;
  justify-content: space-around;
  padding: 10px;
  background-color: #36669d;
  background-image: linear-gradient(315deg, #5a8bc4 0%, #b4e0eb 74%);
  border-radius: 10px;
    
    @media (max-width: 820px) {
      flex-direction: column;
      justify-content: center;
    }
}

.form-group {
  position: relative;
  display: flex;
  justify-content: space-between;
  padding: 10px;
  background-color: #ffffff;
  border-radius: 7px;
  opacity: 0.9;
}

.phone {
  padding-bottom: 32px;

    .error {
      top: 36px;

        @media (max-width: 500px) {
          top: 33px;
        }
    }
}


.gender {
  display: flex;
  gap: 5px;
}

.form__left {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form__left,
.form__right {
  width: 50vw;
  
    @media (max-width: 820px) {
      margin: 0 auto;
      width: 80vw;
    }
    
    @media (max-width: 620px) {
      width: 85vw;
    }

    @media (max-width: 500px) {
      font-size: 12px;
      font-weight: 400;
    }
}

fieldset {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  border: none;
}

legend {
  padding: 0 5px;
  font-weight: 600;
}

[type="text"],
[type="date"],
select {
  padding: 2px 7px;
  width: 25vw;
  border: 1px solid #b5b5b5;
  border-radius: 5px;

    &:focus {
      outline: 2px solid rgb(88, 88, 255);
    }
  
    @media (max-width: 820px) {
      width: 45vw;
    }

    @media (max-width: 820px) {
      width: 40vw;
    }
}

select {
  padding: 2px 7px;
}

button {
  padding: 7px;
  margin: 20px auto;
  width: 50vw;
  background-color: #018ce9;
  color: #fff;
  border: none;
  border-radius: 5px;
  transition: all .2s ease-in;
  cursor: pointer;

    &:hover {
      transform: scale(0.997);
      opacity: 0.8;
    }

    &:disabled {
      transform: scale(0.997);
      opacity: 0.5;
      cursor: not-allowed;
    }
}

.error {
  position: absolute;
  top: 27px;
  left: 10px;
  color: #ff4141;
  font-size: 10px;
}

.modal__content {
  position: relative;
  bottom: 80px;
  left: 0;
  display: block !important;
  margin: 0 auto;
  width: 240px;
  text-align: center;
  font-weight: bold;
  color: rgb(106, 209, 22);
}

</style>
