<template>
  <form @submit.prevent="submitForm">
    <label>Email:</label>
    <input type="email" required autofocus v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="web-developer">Web Developer</option>
      <option value="qa">QA</option>
      <option value="backend-developer">Backend Developer</option>
    </select>

    <!-- <div>
      <p>Select Mentor</p>
      <input type="checkbox" value="pratik" v-model="names">
      <label> Pratik </label>
    </div>
    <div>
      <input type="checkbox" value="kunal" v-model="names">
      <label> Kunal </label>
    </div>
    <div>
      <input type="checkbox" value="pruthvi" v-model="names">
      <label> Pruthvi </label>
    </div> -->

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="removeSkill(skill)">{{skill}}</span>
    </div>


    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and conditions</label>
    </div>

    <input type="submit">
  </form>
  <p>Email: {{email}}</p>
  <p>Password: {{password}}</p>
  <p>Role: {{role}}</p>
  <p>Terms Accepted: {{terms}}</p>
  <p>Skills: {{skills}} </p>
  <!-- <p>{{names}}</p> -->
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'web-developer',
      terms: false,
      // names: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if(e.key === ',' && this.tempSkill) {
        if(!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    submitForm() {
      // validate password
      this.passwordError = this.password.length > 5 ? '' : 'Password must be atleast 6 characters'
    }
  }
}
</script>

<style>
form {
  max-width: 480px;
  background: lightgray;
  margin: 0 auto;
  padding: 30px;
  border-radius: 10px;
}
label{
  display: inline-block;
  text-transform: uppercase;
  margin-top: 20px;
}
input,select {
  display: block;
  box-sizing: border-box;
  margin-top: 10px;
  width: 100%;
  padding: 10px;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
input[type="submit"] {
  margin-top: 10px;
}
p {
  display: block;
  margin-bottom: 1px
}
.pill {
  display: inline-block;
  background: #eee;
  margin: 10px 10px 0 0;
  padding: 6px 12px;
  border-radius: 20px;
  color: #000;
  cursor: pointer;
}
.error {
  color: red;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>