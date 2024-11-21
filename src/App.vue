<template>
  <AppHeaderVue @updateSearch="updateSearch" :searchValue="searchQuery" />
  <main class="app-container">
    <AddFormVue @contactAdded="addContact" :editRow="editRow" />
    <ContactListVue :contacts="filteredContacts" @editContact="editContact" @deleteContact="deleteContact" />
  </main>
</template>

<script>
import AppHeaderVue from './components/AppHeader.vue';
import ContactListVue from './components/ContactList.vue';
import AddFormVue from './components/AddForm.vue';

export default {
  name: "App",
  components: {
    AppHeaderVue,
    ContactListVue,
    AddFormVue,
  },
  data() {
    return {
      contacts: JSON.parse(localStorage.getItem("contacts")) || [],
      searchQuery: "",
      editRow: null, 
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts.filter((contact) => {
        const query = this.searchQuery.toLowerCase();
        return (
          contact.name.toLowerCase().includes(query) ||
          contact.phone.toLowerCase().includes(query)
        );
      });
    }
  },
  methods: {
    addContact(contact) {
      if (this.editRow) {
        const index = this.contacts.findIndex(c => c.id === this.editRow.id);
        if (index !== -1) {
          this.contacts[index] = { ...contact, id: this.editRow.id };
        }
        this.editRow = null;
      } else {
        this.contacts.push(contact);
      }
      this.saveContacts();
    },
    updateSearch(query) {
      this.searchQuery = query;
    },
    saveContacts() {
      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    },
    editContact(contact) {
      this.editRow = contact;
    },
    deleteContact(contactId) {
      this.contacts = this.contacts.filter(contact => contact.id !== contactId);
      this.saveContacts();
    },
  },
};
</script>

<style scoped>
.app-container {
  padding: 30px 40px 10px;
}
</style>
