<template>
  <form @submit.prevent="handleSubmit">
    <label> Email: </label>
    <input
      type="email"
      required
      v-model="email"
      placeholder="Enter your email"
    />
    <div v-if="emailError" class="error">{{ emailError }}</div>
    <label> Password: </label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label>Role:</label>
    <select v-model="role">
      <option value="Web Developer">Web Developer</option>
      <option value="Application Developer">Application Developer</option>
      <option value="Python Developer">Python Developer</option>
    </select>
    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill" />
    <p class="message">Press shift + , to enter a skill</p>
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required />
      <label>Accpet terms and conditions</label>
    </div>

    <!--<div>
      <input type="checkbox" value="Saif" v-model="names" />
      <label>Saif</label>
    </div>
    <div>
      <input type="checkbox" value="Muneeb" v-model="names" />
      <label>Muneeb</label>
    </div>
    <div>
      <input type="checkbox" value="Moni" v-model="names" />
      <label>Moni</label>
    </div>-->
    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
      emailError: "",
      //names:[]
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
      console.log("Skills are: ", this.skills.toString());
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      const REGEXVAR =
        /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password should be at least 6 characters long";

      this.emailError = REGEXVAR.test(this.email) ? "" : "Invalid Email";
    },
  },
};
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
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
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
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8 em;
  font-weight: bold;
}
.message {
  margin: 5px 10px 0 0;
  font-size: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
</style>
