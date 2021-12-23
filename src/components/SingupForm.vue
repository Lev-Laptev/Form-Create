<template>
  <form class="form" @submit.prevent="handlerSubmit">
    <div class="form__wrapper">
      <label class="form__label">Email:</label>
      <input class="form__input" type="email" required v-model="email">
    </div>

    <div class="form__wrapper">
      <label class="form__label">Password:</label>
      <input class="form__input" type="password" required v-model="password">
    </div>

    <div v-if="passwordError" class="form__error"> {{ passwordError }} </div>

    <div class="form__wrapper">
      <label class="form__label">Role:</label>
      <select class="form__input" v-model="role">
          <option value="dev">Developer</option>
          <option value="desig">Designer</option>
      </select>
    </div>

    <div class="form__wrapper">
      <label class="form__label">Skills:</label>
      <input class="form__input" type="text" v-model="tempSkill" @keyup="addSkill">
    </div>

    <div class="form__pill">
      <div v-for="item in skills" :key="item" class="form__item">
        <span @dblclick="deleteSkill(item)">{{ item }}</span>
      </div>
    </div>

    <div class="form__terms">
        <input class="form__checkbox" type="checkbox" required v-model="terms">
        <label class="form__label">Accept terms and conditions</label>
    </div>

    <div class="form__submit">
      <button class="form__button" type="submit">Create an Account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(event) {
      if(event.key === ',' && this.tempSkill) {
        if(!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill.toUpperCase().replace(/,(?=[^,]*$)/, ''))
        }
        this.tempSkill = '' 
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },
    handlerSubmit() {
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'

      if (!this.passwordError) {
        console.log(`email: ${this.email}`);
        console.log(`password: ${this.password}`);
        console.log(`role: ${this.role}`);
        console.log(`skills: ${this.skills}`);
        console.log(`terms accepted: ${this.terms}`);
      }
    }
  },
}
</script>