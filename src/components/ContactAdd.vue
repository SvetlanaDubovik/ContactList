<template>
  <div id="contactAdd" class="contact-add">
    <form class="contact-add__form" @submit.prevent="addNewContact">
      <div class="contact-add__row">
        <div class="contact-add__input-group">
          <input type="text" placeholder="Введите имя" class="contact-add__input" id="name" required v-model="firstName" @keypress="handleInput"/>
          <label for="name">Имя<sup>*</sup></label>
        </div>
        <div class="contact-add__input-group">
          <input type="text" placeholder="Введите фамилию" class="contact-add__input" id="surname" required v-model="lastName" @keypress="handleInput"/>
          <label for="surname">Фамилия<sup>*</sup></label>
        </div>
        <div class="contact-add__input-group">
          <masked-input class="contact-add__input" id="phone" v-model="phoneNumber" mask="\+\7 (111) 111-11-11" placeholder="Введите номер телефона" required/>
          <label for="phone">Телефон<sup>*</sup></label>
        </div>
      </div>
      <p class="contact-add__info">
          * помечены поля, необходимые к заполнению
      </p>
      <div class="contact-add__row_right">
        <button class="contact-add__clear btn" @click="clearForm" type="button">Очистить форму</button>
        <button class="contact-add__add btn" @submit.prevent="addNewContact" type="submit">Сохранить контакт</button>
      </div>
    </form>
  </div>
</template>

<script>
import MaskedInput from 'vue-masked-input'

export default {
  name: 'ContactAdd',
  data () {
    return {
      id: '',
      firstName: '',
      lastName: '',
      phoneNumber: ''
    }
  },
  components: {
    MaskedInput
  },
  methods: {
    addNewContact: function () {
      if (
        this.firstName.length > 0 &&
        this.lastName.length > 0 &&
        this.phoneNumber.length > 0
      ) {
        const firstName = this.firstName
        const lastName = this.lastName
        const phoneNumber = this.phoneNumber
        this.$emit('add-contact', {
          id: `${lastName}-${Date.now()}`,
          firstName,
          lastName,
          phoneNumber
        })
        this.id = ''
        this.firstName = ''
        this.lastName = ''
        this.phoneNumber = ''
      }
    },
    clearForm: function () {
      this.id = ''
      this.firstName = ''
      this.lastName = ''
      this.phoneNumber = ''
    },
    handleInput: function (evt) {
      const regex = new RegExp('^[А-ЯA-Zа-яa-zЁё]+$')
      const key = String.fromCharCode(evt.charCode)
      if (!regex.test(key)) {
        event.preventDefault()
        return false
      }
    }
  }
}
</script>

<style lang="scss">
.contact-add {
  margin-bottom: 40px;
}

.contact-add__form {
  width: 690px;
  margin: 0 auto;
}

.contact-add__input {
  width: 180px;
  padding: 10px;
  padding-right: 0;
  border-radius: 5px;
  box-shadow: none;
}

.contact-add__row {
  display: flex;
  justify-content: space-between;
}

.contact-add__row_right {
  display: flex;
  justify-content: flex-end;
}

.contact-add__info {
  color: red;
  font-size: 12px;
  padding: 10px 0;
  margin: 0;
}

.contact-add__input-group {
  position: relative;
  padding-top: 20px;

  label {
    position: absolute;
    top: 0;
    left: 5px;
    font-size: 16px;
    font-weight: 600;

    sup {
      color: red;
    }
  }
}

.btn {
  padding: 10px;
  border-radius: 5px;
  outline: none;
  cursor: pointer;
}

.contact-add__add {
  margin-left: 20px;
  background: linear-gradient(to top, #009f5d, #00ce74);
  color: #fff;
  font-weight: bold;
  font-size: 16px;
}

.contact-add__clear {
  background-color: #d3d3d3;
  color: rgba(0, 0, 0, 0.7);
}
</style>
