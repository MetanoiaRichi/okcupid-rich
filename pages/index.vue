<template>
	<div 
        id="okc_landing_page" 
        class="is_current_banner_1">

        <div class="page_section_inner w-full max-w-[1180px] pb-16 relative z-[1]">
            <div class="header_section flex items-center justify-between py-8 md:py-12 lg:py-8 md:px-[65px] relative z-[1]">
                <img class="w-[90px]" :src="require('~/assets/svg/ok-cupid-logo.svg')" alt="ok-cupid-logo">

                <div class="header-inner flex items-center">
                    <span class="text-sm text-black mr-6 hidden md:block">Have an account?</span>
                    <el-button 
                        @click="signInDialogVisible = true"
                        class="border border-black bg-transparent w-24 flex-shrink-0 text-black" 
                        plain>
                        Sign In
                    </el-button>
                </div>
            </div>

            <div class="content_section p-0 md:px-[65px] relative z-[1]">
                <h1 id="landing_headline_text" class="text-4xl md:text-6xl font-bold text-white mb-8 tracking-[2px]">
                    DATING FOR EVERY 
                    <br class="hidden lg:inline">SINGLE PERSON
                </h1>

                <div class="img_container lg:hidden mb-8">
                    <img 
                        v-for="i in 4"
                        :key="i"
                        :class="'okc_landing_mob_img_' + i" 
                        :src="require('~/assets/webp/okc_landing_img_mob_' + i +'.webp')" 
                    />
                </div>

                <p class="text_section text-black text-base md:text-xl mb-7">
                    OkCupid is the only dating app that matches you 
                    <br class="hidden lg:inline">on what matters to you. 
                    <br class="hidden lg:inline">You deserve to find who you’re looking for. 
                    <br class="hidden lg:inline">Meet them today!
                </p>

                <p class="text_section text-black text-base text md:text-lg mb-10">
                    By clicking Join, you agree to our 
                    <br class="hidden lg:inline"><a class="text-inherit underline" target="_blank" href="/legal/terms">Terms</a>. Learn how we process your 
                    <br class="hidden lg:inline">data in our <a class="text-inherit underline" target="_blank" href="/legal/privacy">Privacy Policy</a> and 
                    <br class="hidden lg:inline"><a class="text-inherit underline" target="_blank" href="/legal/cookies">Cookies Policy</a>.
                </p>
                
                <NuxtLink to="/signup">
                    <el-button class="font-semibold tracking-[1px] w-full md:w-[284px] bg-black border-0 text-base h-16 text-white mb-6" type="secondary">
                        JOIN OKCUPID
                    </el-button>
                </NuxtLink>

                <div class="install_app_section text-black">
                    <label class="block uppercase font-semibold text-base mb-4">Get the app</label>

                    <div class="flex items-center inner">
                        <a 
                            class="mr-5 cursor-pointer"
                            href="https://play.google.com/store/apps/details?id=com.okcupid.okcupid&amp;referrer=utm_source%3Ddesktophome%2526utm_medium%253Dweb">
                            <img class=" w-[64px] rounded-sm h-[44px] object-cover" src="https://cdn.okccdn.com/media/img/dtf/apps_googleplay2.png" alt="apps_googleplay2">
                        </a>

                        <a 
                            class="mr-5 cursor-pointer"
                            href="https://itunes.apple.com/app/apple-store/id338701294?pt=296162&ct=desktophome%20Score&mt=8">
                            <img class="rounded-sm w-[64px] h-[44px] object-cover" src="https://cdn.okccdn.com/media/img/dtf/apps_apple.png" alt="apps_apple">
                        </a>
                    </div>
                </div>
            </div>

            <div class="img_container hidden lg:inline">
                <img 
                    v-for="i in 4"
                    :key="i"
                    :class="'okc_landing_img_' + i" 
                    :src="require('~/assets/webp/okc_landing_img_' + i +'.webp')" 
                />
            </div>
        </div>

        <SigninForm 
            :signInDialogVisible="signInDialogVisible"
            @close-dialog="signInDialogVisible = false"
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            signInDialogVisible: false,
        }
    },
 	mounted() {
        let counter = 2;
        let el = document.getElementById("okc_landing_page");

        function changeLandingClass() {
            el.className = 'is_current_banner_' + counter;
            if (counter === 4){
                counter = 1;
            } else {
                counter++;
            }
        }

		setInterval(changeLandingClass, 4000);
	},
};
</script>
