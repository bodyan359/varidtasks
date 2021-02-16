<template>
  <div class="home">
    <Table :items="items" v-on:modify="modifyItem" v-on:refresh="refresh"/>
    <Form :item="modified_item" v-on:refresh="refresh"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Form from '@/components/Form.vue'
import Table from '@/components/Table.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Form,
    Table
  },
  data () {
    return {
      items: null,
      modified_item: null
    }
  },
  methods: {
    modifyItem: function (item) {
      this.modified_item = item
    },
    refresh: function () {
      axios.get('http://test01.varid.pl:4080/api/contacts').then(response => {
        this.items = response.data
      })
    }
  },
  mounted () {
    axios
      .get('http://test01.varid.pl:4080/api/contacts')
      .then(response => {
        this.items = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      // eslint-disable-next-line no-return-assign
      .finally(() => this.loading = false)
  }
}
</script>
