<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />
    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div class="error" v-if="passwordError">{{ passwordError }}</div>
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
      <option value="admin">Database Admin</option>
    </select>
    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>
    <div>
      <input type="checkbox" value="inixindo" v-model="names" />
      <label>Inixindo</label>
    </div>
    <div>
      <input type="checkbox" value="yusuf" v-model="names" />
      <label>Yusuf</label>
    </div>
    <div>
      <input type="checkbox" value="rizal" v-model="names" />
      <label>Rizal</label>
    </div>
    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(event) {
      if (event.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      console.log("form submitted!");
      //   validasi terhadap password
      this.passwordError =
        this.password.length >= 6 // ternary operator
          ? ""
          : "Password must be at least 6 chars long!";
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: center;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaaaaa;
  display: inline-block;
  margin: 25px 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  font-weight: bold;
  letter-spacing: 1px;
}
input,
select {
  width: 100%;
  display: block;
  padding: 10px 6px;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #dddddd;
  color: #555555;
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
  background: #eeeeee;
  border-radius: 20px;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  color: #777777;
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
  color: #ff0060;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>