<template>
  <div>

    <div class="primary-heading-con">
      <div class="container">
          <div class="is-size-5 has-text-weight-bold">Stocks:</div>
      </div>
    </div>

  </div>
</template>

<script>
import API from '../api/IEX';
export default {
    name : "Symbols",
    data () {
        return {
            loading : true,
            companies : [],
        };
    },
    beforeMount () {
        API.getCompanies().then(response => {
            this.companies = response.data;
        }).finally(() => {
            this.loading = false;
        });
    },
}
</script>

<style lang="scss" scoped>
.app .primary-heading-con {
  width: 100vw;
  padding: 4px 7px;
}
</style>
