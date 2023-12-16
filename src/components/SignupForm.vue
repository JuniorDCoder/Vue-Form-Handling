<template>
    <form @submit.prevent="handleSubmit">
        <label for="email">Email: </label>
        <input v-model="email" @input="emailTouched = true" required type="email">
        <p class="error" v-if="emailError">{{ emailError }}</p>
        <p class="success" v-else-if="emailTouched && !emailError">✔ Email is valid</p>
        <!-- ... -->
        <label for="password">Password: </label>
        <input v-model="password" @input="passwordTouched = true" required type="password">
        <p class="error" v-if="passwordError">{{ passwordError }}</p>
        <p class="success" v-else-if="passwordTouched && !passwordError">✔ Password is valid</p>

        <label>Role: </label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Designer</option>
        </select>

        <label for="">Skills</label>
        <input v-model="tempSkill" type="text" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            {{ skill }}
            <button @click="removeSkill(skill)" class="cancel-button">X</button>
        </div>

        <div class="terms">
            <input v-model="terms" @change="termsTouched = true" type="checkbox" required>
            <label for="">Accept Terms and Conditions</label>
            <p class="error" v-if="termsError">{{ termsError }}</p>
            <p class="success" v-else-if="termsTouched && !termsError">✔ Terms are accepted</p>
        </div>
        <div class="submit">
            <button class="create-account-button">Create an Account</button>
        </div>
    </form>
</template>

<script>
export default{
    data(){
        return{
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkill: '',
            skills: [],
            emailTouched: false,
            passwordTouched: false,
            termsTouched: false,
        }
    },
    methods: {
        addSkill(event){
            if ((event.key === ',' || event.key === 'Enter') && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                    
                }
                this.tempSkill = ''
            }
        },
        removeSkill(skill){
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
            // Additionally we could pass "index" in the function call then execute this.skills.splice(index, 1)
        },
        handleSubmit(){
        
        },
    },
    computed: {
        emailError() {
            if (!this.emailTouched) {
                return null;
            } else if (!this.email) {
                return "Email is required";
            } else if (!/\S+@\S+\.\S+/.test(this.email)) {
                return "Email is invalid";
            } else {
                return null;
            }
        },
        passwordError() {
            if (!this.passwordTouched) {
                return null;
            } else if (!this.password) {
                return "Password is required";
            } else if (this.password.length < 8) {
                return "Password must be at least 8 characters";
            } else {
                return null;
            }
        },
        termsError() {
            if (!this.termsTouched) {
                return null;
            } else if (!this.terms) {
                return "You must accept the terms and conditions";
            } else {
                return null;
            }
        }
    },
}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    padding: 10px;
    background-color: #f2f2f2;
    margin: 5px;
    border-radius: 20px;
}

.cancel-button {
    background: none;
    border: none;
    cursor: pointer;
    margin-left: 10px;
    color: red;
}
.create-account-button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 4px;
    transition-duration: 0.4s;
}

.create-account-button:hover {
    background-color: white; 
    color: black; 
    border: 2px solid #4CAF50;
}
.error {
    color: red;
    margin-top: 5px;
    font-size: 16px;
    font-style: italic;
}
.success {
    color: green;
    margin-top: 5px;
}
</style>