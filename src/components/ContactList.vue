<template>
  <ul id="contactList" class="contact-list" >
    <ContactItem @delete-contact="deleteContact"  v-for="(contact) in contacts" :contact.sync="contact" :key="contact.id"/>
  </ul>
</template>

<script>
import ContactItem from './ContactItem'

export default {
  name: 'ContactList',
  components: {
    ContactItem
  },
  props: ['contacts'],
  methods: {
    deleteContact (contact) {
      this.$emit('delete-contact', contact)
    }
  }
}
</script>

<style lang="scss">
.contact-list {
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0;

  &__item:nth-of-type(odd) {
    background-color: #fff;
  }

  &__item:nth-of-type(even) {
    background-color: #f7f7f7;
  }
}
</style>
