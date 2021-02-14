<template>
  <div>
    <b-form @submit="postData" @modify="putData" v-if="show">
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

    <b-form-group id="input-group-2" label="Your last_name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.last_name"
          placeholder="Enter last_name"
          required
        ></b-form-input>
      </b-form-group>

          <b-form-group id="input-group-2" label="Your number:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.phone_number"
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

          <b-form-group id="input-group-2" label="Your address:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.address"
          placeholder="Enter address"
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
      <b-button type="modify" variant="danger">Modify</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

// name, last name, phone number, email, country, city, address

<script>
import axios from 'axios'

export default {
  name: 'Form',
  props: {
    item: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      form: {
        email: '',
        name: '',
        last_name: '',
        phone_number: '',
        country: '',
        address: '',
        city: ''
      },
      show: true
    }
  },
  methods: {
    postData () {
      axios.post('http://test01.varid.pl:4080/api/contact', this.form)
        .then(async response => {
          await axios.get('http://test01.varid.pl:4080/api/contacts').then(response => {
            this.items = response.data
          })
        })
        .catch(function (error) {
          alert(error)
        })
    },
    putData () {
      axios.put('http://test01.varid.pl:4080/api/contact', this.form)
        .then(async response => {
          await axios.get('http://test01.varid.pl:4080/api/contacts').then(response => {
            this.items = response.data
          })
        })
        .catch(function (error) {
          alert(error)
        })
    },
    onReset (event) {
      event.preventDefault()
      // Reset our form values
      this.form.email = ''
      this.form.name = ''
      this.form.last_name = ''
      this.form.phone_number = ''
      this.form.country = ''
      this.form.address = ''
      this.form.city = ''
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    },
    modifyData () {
      axios.post('', this.form).then(response => {
        this.$emit('refresh')
      })
    }
  },
  watch: {
    item: function () {
      this.form.email = this.item.email
      this.form.name = this.item.name
      this.form.last_name = this.item.last_name
      this.form.phone_number = this.item.phone_number
      this.form.country = this.item.country
      this.form.address = this.item.address
      this.form.city = this.item.city
    }
  }
}
</script>
