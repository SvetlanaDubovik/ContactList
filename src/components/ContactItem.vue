<template>
  <li class="contact-list__item contact-item">
    <div class="contact-item__initials">
      <span>{{getInitials(contact.firstName, contact.lastName)}}</span>
    </div>
    <div class="contact-item__name">{{contact.firstName}}</div>
    <div class="contact-item__surname">{{contact.lastName}}</div>
    <div class="contact-item__phone">
      <a :href="`tel:${ contact.phoneNumber }`">{{contact.phoneNumber}}</a>
    </div>
    <div class="contact-item__delete">
      <button class="contact-item__delete_button" title="Удалить контакт" @click="deleteContact(contact)">
        <img src="../assets/DeleteRed.png" alt="Удалить контакт" width="20" height="20">
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: 'ContactItem',
  props: ['contact'],
  methods: {
    deleteContact (contact) {
      this.$emit('delete-contact', contact)
    },
    getInitials (firstName, lastName) {
      return (
        firstName.slice(0, 1).toUpperCase() + lastName.slice(0, 1).toUpperCase()
      )
    }
  }
}
</script>

<style lang="scss">
.contact-item {
  position: relative;
  padding: 10px 0;
  font-size: 16px;
  line-height: 50px;
  display: flex;
  justify-content: space-around;
}

.contact-item__initials {
  display: inline-block;
  flex-basis: 20%;
  color: #2478ad;
  font-weight: 600;
  font-size: 18px;

  span {
    margin: 0 auto;
    display: block;
    text-align: center;
    width: 50px;
    height: 50px;
    background-color: #d3d3d3;
    border-radius: 50%;
  }
}

.contact-item__name,
.contact-item__surname,
.contact-item__phone,
.contact-item__delete {
  flex-basis: 20%;
  display: inline;
  vertical-align: middle;
  text-align: center;
  color: #2478ad;
  font-weight: 600;
}

.contact-item__phone {
  a {
    text-decoration: none;
    color: #2478ad;
  }
}

.contact-item__delete {
  position: relative;
}

.contact-item__delete_button {
  position: absolute;
  border: none;
  outline: none;
  background-color: transparent;
  cursor: pointer;
  top: 10px;
  left: 50%;

  img {
    width: 20px;
    height: 20px;
  }
}
</style>
