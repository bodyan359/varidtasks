<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

    <b-form-group id="input-group-2" label="Your lastname:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.lastname"
          placeholder="Enter lastname"
          required
        ></b-form-input>
      </b-form-group>

          <b-form-group id="input-group-2" label="Your number:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.number"
          placeholder="Enter number"
          required
        ></b-form-input>
      </b-form-group>

          <b-form-group id="input-group-2" label="Your country:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.country"
          placeholder="Enter country"
          required
        ></b-form-input>
      </b-form-group>

          <b-form-group id="input-group-2" label="Your adress:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.adress"
          placeholder="Enter adress"
          required
        ></b-form-input>
      </b-form-group>

          <b-form-group id="input-group-2" label="Your city:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.city"
          placeholder="Enter city"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Add new item</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

// name, last name, phone number, email, country, city, address

<script>
export default {
  name: 'Form',
  data () {
    return {
      form: {
        email: '',
        name: '',
        lastname: '',
        number: '',
        country: '',
        adress: '',
        city: ''
      },
      show: true
    }
  },
  methods: {
    onSubmit (event) {
      event.preventDefault()
      alert(JSON.stringify(this.form))
    },
    onReset (event) {
      event.preventDefault()
      // Reset our form values
      this.form.email = ''
      this.form.name = ''
      this.form.lastname = ''
      this.form.number = ''
      this.form.country = ''
      this.form.adress = ''
      this.form.city = ''
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
}
</script>
