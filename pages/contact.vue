<template>
  <div>
    <SecondNav></SecondNav>
    <div class="container" id="form-container">
        <input type="text" v-model="name" placeholder="Name" class="col align-self-center global-input">
        <input type="email" v-model="email" placeholder="Email" class="col align-self-center global-input">
        <input type="text" v-model="subject" placeholder="Subject" class="col align-self-center global-input">
        <textarea v-model="question" id="" cols="30" rows="10" class="col align-self-center global-input" placeholder="Help us help you"> Help us help you</textarea>
        <button @click.prevent="submitForm" class="btn-main btn col align-self-center">SUBMIT</button>
        <button @click.prevent="resetFields" class="btn-main btn col align-self-center">RESET</button>
    </div>
  </div>
</template>

<script>
import SecondNav from '@/components/SecondNav'

  export default {
    data() {
      return {
          email: "",
          name: "",
          subject: "",
          question: ""
        }
    },
    methods: {
      async submitForm() {
        let newQuestion = {
          email: this.email,
          name: this.name,
          subject: this.subject,
          question: this.question
        }
        try {
          const response = await this.$axios.post('send-email', newQuestion)
          this.resetFields()
        } catch (error) {
          alert(err.message)
        }
      },
      resetFields() {
        // Reset form values
        this.email = ""
        this.name = ""
        this.subject = ""
        this.question= ""
        }
      },
    components: {
      SecondNav
    }
  }
</script>

