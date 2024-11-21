<template>
    <template v-if="contacts.length">
        <table class="app-table">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Fullname</th>
                    <th>Phone Number</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(contact, index) in contacts" :key="contact.id">
                    <td>{{ index + 1 }}</td>
                    <td>{{ contact.name }}</td>
                    <td>{{ contact.phone }}</td>
                    <td>
                        <AppButton text="Edit" buttonType="warning" @click="editContact(contact)" />
                        <AppButton text="Delete" buttonType="danger" @click="deleteContact(contact.id)" />
                    </td>
                </tr>
            </tbody>
        </table>
        <p class="app-table-count">Count: {{ contacts.length }}</p>
    </template>
    <div v-else class="app-empty-box">
        <p>No item to display ...</p>
    </div>
</template>

<script>
import AppButton from './../components/form/AppButton.vue';

export default {
    name: "Contact-List",
    props: ["contacts"],
    components: {
        AppButton
    },
    methods: {
        editContact(contact) {
            this.$emit('editContact', contact);
        },
        deleteContact(contactId) {
            this.$emit('deleteContact', contactId);
        },
    },
};
</script>


<style scoped>
.app-empty-box {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 5px;
    min-height: 100px;
    background: rgba(0, 0, 0, 0.1);
}

.app-empty-box {
    letter-spacing: 1px;
    font-size: 20px;
}

.app-table {
    width: 100%;
    border-radius: 5px;
}

.app-table tbody {
    display: flex;
    flex-direction: column;
}

.app-table-count {
    font-size: 15px;
    letter-spacing: 1px;
}

.app-table tr {
    display: flex;
    align-items: center;
}

.app-table tbody tr {
    padding: 5px;
    border: 1px solid;
    margin-bottom: -1px;
}

.app-table thead tr {
    padding: 5px 5px 10px;
}

.app-table td,
.app-table th {
    flex: 1;
}

.app-table td {
    justify-content: center;
    display: flex;
    text-align: center !important;
}
</style>
