<template>
	<main>
        <LoadingAnimation :style="showLoadingAnim ? '' : 'display: none !important'"/>
		<Nuxt />
		<FooterNavigation />
	</main>
</template>


<script>
    export default {
        beforeCreate() {
            this.showLoadingAnim = true;
        },
        mounted() {
            setTimeout(() => this.showLoadingAnim = false, 2000); 
        },
        data() {
            return {
                showLoadingAnim: true,
            };
        },
    };
</script>

<style lang="scss">
    @import "~/assets/scss/overrides.scss";
</style>