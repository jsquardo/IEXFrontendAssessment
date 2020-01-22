<template>
  <div class="container">
		<Nav />
    <HeroSection />
  </div>
</template>

<script>
import API from "../api/IEX";
import Nav from "../components/Nav";
import HeroSection from '../components/HeroSection'

export default {
	name: "Symbols",
	components: {
    Nav,
    HeroSection
	},
	data() {
		return {
			loading: true,
			companies: []
		};
	},
	beforeMount() {
		API.getCompanies().then(response => {
        this.companies = response.data;
			})
			.finally(() => {
				this.loading = false;
			});
	}
};
</script>
