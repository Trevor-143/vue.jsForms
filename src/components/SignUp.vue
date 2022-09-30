<template>
  <form @submit.prevent="submitted">
    <input type="email" v-model="email" placeholder="email" id="email">
    <input type="password" v-model="password" placeholder="password" id="password">
    <div v-if="passwordError" class="error">{{passwordError}}</div>
    <select v-model="whatTheyDo">
        <option value="developer">Developer</option>
        <option value="Designer">Designer</option>
        <option value="Programmer">Programmer</option>
        <option value="UX Designer">UX Designer</option>
        <option value="Animator">Animator</option>
    </select>

    <label class="skill">Skills</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div class="ski">
        <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
            {{skill}} 
        </div>
    </div>

    <div class="terms">
        <input type="checkbox" required v-model="terms">
        <label>Check for terms and conditions..</label>
    </div>
    <button>Click to sign up</button>
  </form>
  <div class="output">
    <h4>Your Email: {{email}} </h4>
    <h4>Your Password: {{password}} </h4>
    <h4>What You Do: {{whatTheyDo}} </h4>
    <h4>Accepted terms: {{terms}} </h4>
  </div>

  
</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            passwordError: "",
            whatTheyDo: "",
            terms: false,
            tempSkill: "",
            skills: []
        }
    },
    methods: {
        addSkill(e) {
            // console.log(e)
            if(e.key === "," && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill);
                }
                this.tempSkill = ""
            }
        },
        removeSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        submitted() {
            // for the password
            this.passwordError = this.password.length > 8 ? 
            '' : 'Please enter more than 8 characters fro the password.'
            if(!this.passwordError) {
                console.log('here is the inform')
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('What you do: ', this.whatTheyDo)
                console.log('The skills: ', this.skills)
                console.log('Accepted terms: ', this.terms)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 400px;
        width: 100%;
        margin: 30px auto;
        padding: 25px;
        background: #ffffff;
        border-radius: 7px;
        box-shadow: 0px 5px 28px 20px rgb(0 0 0 / 10%);
    }
    input {
        padding: 12px;
        border-radius: 7px;
        border: none;
        width: 100%;
        margin: 15px 0;
        background: #f0f0f0;
        box-sizing: border-box;
    }
    input::placeholder {
        color: #b9b9b9;
    }
    input:focus {
        outline: none;
    }
    select {
        padding: 8px 13px;
        background: #dcdbff;
        color: #4e4e4e;
        border: none;
        border-radius: 7px;
    }
    .terms {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        margin: 10px 0;
    }
    input[type="checkbox"] {
        margin: 0 10px 0 0 ;
        width: 20px;
    }
    .skill {
        display: inline-block;
        width: 100%;
        margin-top: 20px;
    }
    .ski {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
        cursor: pointer;
    }
    .pill {
        padding:7px 13px;
        margin: 5px;
        width: fit-content;
        border-radius: 20px;
        background: rgb(52, 44, 170);
        color: #ffffff;
    }
    button {
        padding: 7px 14px;
        width: fit-content;
        margin: 10px auto;
        background: #241481;
        color: #ffffff;
        border-radius: 20px;
        border: none;
        cursor: pointer;
    }
    .error {
        padding: 6px 10px;
        margin: 5px;
        background: rgb(168, 0, 0);
        color: #ffffff;
        border-radius: 7px;
    }
</style>