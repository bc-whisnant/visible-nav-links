<template>
  <b-navbar toggleable="md" type="dark" variant="dark">
    <b-dropdown id="ddown1" text="Companies" class="m-md-2">
      <div>
        <menu-item v-for="(item, index) in visibleCompany" :key="index" :text="item.id"></menu-item>
      </div>
    </b-dropdown>
    <b-dropdown id="ddown1" text="Testing" class="m-md-2">
      <div>
        <menu-item v-for="(item, index) in visiblePlaces" :key="index" :text="item.id"></menu-item>
      </div>
      <b-dropdown-divider></b-dropdown-divider>
      <b-dropdown-header>TRC</b-dropdown-header>
      <div>
        <menu-item v-for="(item, index) in visiblePlacesTrc" :key="index" :text="item.id"></menu-item>
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
    visibleCompany: function() {
      return this.linksToFilter.filter(function(link) {
          let visibleCompany = link.visible === true && link.section === 'company'
          return visibleCompany
      })
    },
    visiblePlaces: function() {
    return this.linksToFilter.filter(function(link) {
          let visiblePlaces = link.visible === true && link.section === 'places'
          return visiblePlaces
      })
    },
    visiblePlacesTrc: function() {
    return this.linksToFilter.filter(function(link) {
          let visiblePlacesTrc = link.visible === true && link.section === 'placesTrc'
          return visiblePlacesTrc
      })
    }
  }, 
}
</script>

<style>

</style>
