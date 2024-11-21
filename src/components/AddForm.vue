<template>
    <form class="App-Form" @submit.prevent="addContact">
        <div class="app-input-root">
            <label for="">Full Name:</label>
            <div class="app-input">
                <input v-model="name" type="text" placeholder="Please enter the full name ... ">
            </div>
            <p v-if="errors.name" class="app-input-error">{{ errors.name }}</p>
        </div>
        <div class="app-input-root">
            <label for="">Phone Number:</label>
            <div class="app-input">
                <input v-model="phone" type="text" placeholder="Please enter the number ... ">
            </div>
            <p v-if="errors.phone" class="app-input-error">{{ errors.phone }}</p>
        </div>
        <div class="app-form-actions">
            <AppButton type="button" v-if="!editRow" text="Reset" buttonType="outline" @click="resetForm" />
            <AppButton type="submit" :text="editRow ? 'Update' : 'Save'" buttonType="primary" />
        </div>
    </form>
</template>

<script>
import AppButton from './../components/form/AppButton.vue';

export default {
    name: "Add-Form",
    props: ["editRow"],
    emits: ["contactAdded"],
    components: { AppButton },
    data() {
        return {
            name: this.editRow ? this.editRow.name : "",
            phone: this.editRow ? this.editRow.phone : "",
            errors: {
                name: "",
                phone: ""
            },
        };
    },
    watch: {
        editRow(newVal) {
            this.name = newVal ? newVal.name : "";
            this.phone = newVal ? newVal.phone : "";
            this.errors = { name: "", phone: "" };
        }
    },
    methods: {
        addContact() {
            this.errors = { name: "", phone: "" };
            let valid = true;

            if (!this.name) {
                this.errors.name = "Full Name is required!";
                valid = false;
            }

            if (!this.phone) {
                this.errors.phone = "Phone Number is required!";
                valid = false;
            } else if (!/^\d{10}$/.test(this.phone)) {
                this.errors.phone = "Phone Number must be 10 digits!";
                valid = false;
            }

            if (!valid) return;

            const newContact = {
                name: this.name,
                phone: this.phone,
                id: this.editRow ? this.editRow.id : Date.now(),
            };

            this.$emit("contactAdded", newContact);
            this.resetForm();
        },
        resetForm() {
            this.name = "";
            this.phone = "";
            this.errors = { name: "", phone: "" };
        }
    },
};
</script>


<style scoped>
.App-Form {
    margin-bottom: 30px;
    width: fit-content;
    display: flex;
    align-items: start;
    column-gap: 18px;
    row-gap: 2px;
    flex-wrap: wrap;
}

.app-form-actions {
    display: flex;
    align-items: center;
    margin-top: 38px;
    gap: 6px;
}

.App-Form .app-btn {
    min-width: 80px;
    max-height: 41px;
    min-height: 41px;
}

.app-input-root {
    margin: 16px 0 6px 0;
    display: flex;
    flex-direction: column;
    row-gap: 3px;
}

.app-input-root label {
    font-size: 15px;
    letter-spacing: 0.7px;
}

.app-input input {
    outline: unset !important;
    border: unset !important;
    background: transparent;
    min-width: 300px;
}

.app-input {
    padding: 12px 8px;
    border-radius: 5px;
    background: rgba(0, 0, 0, 0.13);
}

.app-input-error {
    margin: 0;
    margin-top: -2px;
    font-size: 14px;
    color: #bf3100;
    letter-spacing: 0.8px;
}
</style>