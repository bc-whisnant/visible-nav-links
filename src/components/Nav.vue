<template>
  <b-navbar toggleable="md" type="dark" variant="dark">
    <b-dropdown id="ddown1" text="Companies" class="m-md-2">
      <div>
        <menu-item v-for="(item, index) in visible" :key="index" :text="item.id"></menu-item>
      </div>
    </b-dropdown>
  </b-navbar>
</template>

<script>
import MenuItem from './MenuItem'
import axios from 'axios'
export default {
  name: 'Nav',
  data() {
    return {
      items: [
        'Home Builders',
        'Program Sponsors',
        'Providers',
        'Rating Companies',
        'Utility Companies',
        'HVAC Contractors',
        'QA/QC Companies',
        'General Companies',
        'EPA Directory'
      ],
      linksToFilter: []
    }
  },
  components: {
    MenuItem
  },
  mounted () {
    axios.get('http://localhost:3000/links')
      .then(response => {
        this.linksToFilter = response.data
      })
  },
  computed: {
    visible: function() {
      return this.linksToFilter.filter(function(link) {
        let visible = link.visible === true
        return visible
      })
    }
  }
}
</script>

<style>

</style>
