<template>
  <div id="app" class="contacts">
    <h1 class="contacts__title">Список контактов</h1>
    <ContactAdd @add-contact="addContact"/>
    <ContactList :contacts="sortedContacts" @delete-contact="deleteContact"/>
  </div>
</template>

<script>
import ContactAdd from './ContactAdd'
import ContactList from './ContactList'
import 'normalize.css'

export default {
  name: 'app',
  components: {
    ContactAdd,
    ContactList
  },
  data () {
    return {
      contacts: []
    }
  },
  computed: {
    sortedContacts () {
      const copyContacts = this.contacts.slice()
      return copyContacts.sort(sortByLastName)
    }
  },
  mounted () {
    if (localStorage.getItem('contacts')) {
      try {
        this.contacts = JSON.parse(localStorage.getItem('contacts'))
      } catch (e) {
        localStorage.removeItem('contacts')
      }
    } else {
      // чтобы изначально были видны какие-нибудь данные
      this.contacts = initialContacts
      localStorage.setItem('contacts', JSON.stringify(this.contacts))
    }
  },
  beforeUpdate () {
    if (this.contacts.length === 0) {
      localStorage.removeItem('contacts')
    } else {
      const stringifyContacts = JSON.stringify(this.contacts)
      localStorage.setItem('contacts', stringifyContacts)
    }
  },
  methods: {
    addContact (newContact) {
      this.contacts.push(newContact)
    },
    deleteContact (contact) {
      const contactIndex = this.contacts.indexOf(contact)
      this.contacts.splice(contactIndex, 1)
    }
  }
}

const sortByLastName = (a, b) => {
  return a.lastName.toLowerCase() > b.lastName.toLowerCase()
}

const initialContacts = [
  {
    id: 'Иванов-1538308376261',
    firstName: 'Иван',
    lastName: 'Иванов',
    phoneNumber: '+7(922) 322-42-52'
  },
  {
    id: 'Петров-1538308376262',
    firstName: 'Алексей',
    lastName: 'Петров',
    phoneNumber: '+7(902) 322-42-52'
  },
  {
    id: 'Сидоров-1538308376261',
    firstName: 'Александр',
    lastName: 'Сидоров',
    phoneNumber: '+7(912) 322-42-52'
  }
]
</script>

<style lang="scss">
html, body {
  background-color: #edeae5;
}

.contacts {
  background-color: #f7f7f7;
  width: 800px;
  margin: 0 auto;
  border: 1px solid #d3d3d3;
  min-height: 100vh;

  &__title {
    line-height: 0.5;
    text-align: center;
    margin: 0 0 20px;
    padding: 30px 0;
    background: linear-gradient(to top, #297aaf, #44a6e7);
    color: #fff;
  }
}
</style>
