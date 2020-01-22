<template>
  <div class="columns">
    <div class="column is-half">
      <div class="container">
        <p class="has-text-centered title is-1 m-v-lg">Top Gainers</p>
        <div class="center-it">
          <vuetable ref="vuetable"
            api-url="getGainers()"
            :fields="fields"
            :api-mode="false"
            :data="gainers"
            :sort-order="sortOrder"
            :css="css.table"
            :query-params="makeQueryParams"
            :show-sort-icons="true"
          ></vuetable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import FieldsDef from '../../src/api/util/FieldsDef.js'
import API from "../api/IEX";
import Vuetable from "vuetable-2/src/components/Vuetable";
export default {
	name: "HeroSection",
  components: {
    Vuetable
  },
	data() {
		return {
			loading: true,
      gainers: [],
      fields: [
        {
          name: 'companyName',
          sortField: 'name'
        },
        {
          name: 'high',
          sortField: 'high'
        }
      ],
      css: {
        table: {
          tableClass: 'table table-striped table-bordered table-hovered',
          loadingClass: 'loading',
          ascendingIcon: 'glyphicon glyphicon-chevron-up',
          descendingIcon: 'glyphicon glyphicon-chevron-down',
          handleIcon: 'glyphicon glyphicon-menu-hamburger',
        }
      }
		};
  },
  methods: {
    makeQueryParams (sortOrder, currentPage, perPage) {
      return {
        sortBy: sortOrder[0].field
      }
    }
  },
	beforeMount() {
		API.getGainers()
			.then(response => {
				this.gainers = response.data;
			})
			.finally(() => {
				this.loading = false;
			});
	}
};
</script>

<style lang="css">
.center-it {
  display: flex;
  justify-content: center
}
</style>