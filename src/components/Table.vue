<template>
<div>
       <b-table sticky-header striped :fields="fields" :items="items">
             <template #cell(functions)="row" >
             <b-button class="m-0" variant="success" v-on:click="modifyData(row.item.id)">
                Modify
             </b-button>
             <b-button class="m-1" variant="danger"  v-on:click="deleteData(row.item.id)">
                Remove
             </b-button>
            </template>

       </b-table>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Table',
  props: {
    items: null
  },
  data () {
    return {
      fields: ['name', 'last_name', 'phone_number', 'email', 'country', 'city', 'address', 'functions']
    }
  },
  methods: {
    debug (e) {
      console.log(e)
    },
    modifyData: function (id) {
      this.$emit('modify', this.items.filter(item => item.id === id)[0])
    },
    deleteData: function (id) {
      axios.delete('http://test01.varid.pl:4080/api/contact/delete/' + id)
        .then(
          axios.get('http://test01.varid.pl:4080/api/contacts').then(response => {
            // eslint-disable-next-line no-unused-vars
            let newData = this.items
            newData = response.data
            this.$emit('refresh', newData)
          })
        )
    }
  }
}
</script>
