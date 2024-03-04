<template>
    <form @submit.prevent="handleSubmit">
        <TextInput label="First Name" v-model="firstName" :error="firstNameErr" input-id="first-name" />

        <TextInput label="Last Name" v-model="lastName" :error="lastNameErr" input-id="last-name" />

        <EmailInput v-model="email" :error="emailErr" />

        <PhoneInput :prefix="phonePrefix" :number="phoneNum" :error="phoneErr" @update:prefix="phonePrefix = $event"
            @update:number="phoneNum = $event" />

        <PasswordInput v-model="password" :error="passwordErr" />

        <div class="submit">
            <button type="submit">Submit</button>
        </div>
    </form>
</template>

<script>
import TextInput from './TextInput.vue';
import EmailInput from './EmailInput.vue';
import PhoneInput from './PhoneInput.vue';
import PasswordInput from './PasswordInput.vue';

export default {
    components: {
        TextInput,
        EmailInput,
        PhoneInput,
        PasswordInput
    },
    data() {
        return {
            firstName: '',
            lastName: '',
            email: '',
            phonePrefix: '',
            phoneNum: '',
            password: '',

            firstNameErr: '',
            lastNameErr: '',
            emailErr: '',
            phoneErr: '',
            passwordErr: ''
        }
    },
    methods: {
        handleSubmit() {
            const formData = {
                firstName: this.firstName,
                lastName: this.lastName,
                email: this.email,
                phone: `${this.phonePrefix}-${this.phoneNum}`,
                password: this.password
            }

            const validFirstName = this.isValidFirstName();
            const validLastName = this.isValidLastName();
            const validEmail = this.isValidEmail();
            const validPhone = this.isValidPhone();
            const validPassword = this.isValidPassword();

            if (validFirstName && validLastName && validEmail && validPhone && validPassword) {
                console.log(formData)
            }

        },

        isValidFirstName() {
            this.firstNameErr = '';
            const onlyLetters = /^[A-Za-z]+$/.test(this.firstName);
            if (!onlyLetters) {
                this.firstNameErr += 'First name must contain only letters. ';
            }

            const validLength = this.firstName.length > 2 && this.firstName.length < 12;
            if (!validLength) {
                this.firstNameErr += 'First name must be between 2 and 12 characters.';
            }

            return (onlyLetters && validLength);
        },


        isValidLastName() {
            this.lastNameErr = '';
            const onlyLetters = /^[A-Za-z]+$/.test(this.lastName);
            if (!onlyLetters) {
                this.lastNameErr += 'Last name must contain only letters. ';
            }

            const validLength = this.lastName.length > 2 && this.lastName.length < 15;
            if (!validLength) {
                this.lastNameErr += 'Last name must be between 2 and 15 characters.';
            }

            return (onlyLetters && validLength);
        },

        isValidEmail() {
            this.emailErr = '';
            const validEmail = /^[^@]+@\w+(\.\w+)+\w$/.test(this.email);
            if (!validEmail) {
                this.emailErr = 'Invalid email';
            }
            return validEmail;
        },

        isValidPhone() {
            this.phoneErr = '';
            const length = this.phoneNum.length === 7;
            if (!length) {
                this.phoneErr = 'Phone number must be 7 digits. ';
            }

            const containsOnlyNumbers = this.phoneNum.match(/^[0-9]+$/);
            if (!containsOnlyNumbers) {
                this.phoneErr += 'Phone number must contain only numbers. ';
            }

            const prefix = this.phonePrefix !== '';
            if (!prefix) {
                this.phoneErr += 'A valid prefix must be selected. ';
            }

            return (length && containsOnlyNumbers && prefix);
        },

        isValidPassword() {
            this.passwordErr = '';
            const length = this.password.length > 7;
            if (!length) {
                this.passwordErr = 'Must be at least 8 characters long. ';
            }

            const containsUppercase = /[A-Z]/.test(this.password);
            if (!containsUppercase) {
                this.passwordErr += 'Must contain at least one uppercase letter. ';
            }

            const containsLowercase = /[a-z]/.test(this.password);
            if (!containsLowercase) {
                this.passwordErr += 'Must contain at least one lowercase letter. ';
            }

            const containsNumber = /[0-9]/.test(this.password);
            if (!containsNumber) {
                this.passwordErr += 'Must contain at least one number. ';
            }

            const containsSpecial = /[#?!@$%^&*-]/.test(this.password);
            if (!containsSpecial) {
                this.passwordErr += 'Must contain at least one special character. ';
            }

            return (length && containsUppercase && containsLowercase && containsNumber && containsSpecial);
        }
    },
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

.phoneNum {
    display: flex;
    align-items: center;
}

.phoneNum select {
    padding: 10px 6px;
    width: 100px;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    margin-right: 10px;
}

.phoneNum #number {
    margin-left: 10px;
}

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}

.submit {
    text-align: center;
}

.error {
    color: red;
    font-size: 0.8em;
    margin-top: 10px;
    font-weight: bold;
}
</style>