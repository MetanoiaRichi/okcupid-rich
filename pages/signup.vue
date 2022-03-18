<template>
    <div 
        id="okc_signup_page"
        class="bg-[#f0f2f6] px-10 md:px-14 lg:px-16 min-h-screen pb-16">
        
        <div class="header_section py-8 lg:px-64 md:py-12 lg:py-8">
            <img class="w-[90px]" :src="require('~/assets/svg/ok-cupid-logo.svg')" alt="ok-cupid-logo">
        </div>

        <div class="page_section_inner w-full flex flex-col min-h-[80vh] justify-center items-center">
            <div class="panel_one py-10 md:px-[65px] text-center relative w-full max-w-[500px]" v-if="!isStepTwo">
                <NuxtLink 
                    class="cursor-pointer text-[color:var(--blue)] absolute top-0 left-0"
                    to="/">
                    <i class="is_bold el-icon-arrow-left go_back text-2xl"></i>
                </NuxtLink>

                <div class="head mb-16">
                    <p class="text-lg font-medium mb-4">About you</p>
                    <h1 class="text-3xl font-semibold text-[color:var(--gray)]">Welcome! <br class="md:hidden">Who are you?</h1>
                </div>

                <el-form class="mb-28">
                    <el-form-item label="Email" required>
                        <el-input type="text" v-model="email" placeholder="Email"></el-input>
                    </el-form-item>

                    <el-form-item>
                        <el-checkbox
                            class="mt-2"
                            label="I don‘t want to miss discounts & promotional emails from OkCupid"
                            v-model="promotions">
                        </el-checkbox>
                    </el-form-item>
                </el-form>

                <el-button 
                    :disabled="email.trim() == ''"
                    @click="isStepTwo = true"
                    class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                    Next
                </el-button>
            </div>

            <div class="panel_two py-10 md:px-[65px] text-center relative w-full max-w-[500px]" v-else>
                <div
                    @click="isStepTwo = false"
                    class="cursor-pointer text-[color:var(--blue)] absolute top-0 left-0">
                    <i class="is_bold el-icon-arrow-left go_back text-2xl"></i>
                </div>

                <div class="head mb-16">
                    <p class="text-lg font-medium mb-4">About you</p>
                    <h1 class="text-3xl font-semibold text-[color:var(--gray)]">Create a password</h1>
                </div>

                <el-form class="mb-28">
                    <el-form-item label="Password" required>
                        <el-input type="password" v-model="password" placeholder="6 characters minimum"></el-input>
                    </el-form-item>
                </el-form>

                <NuxtLink to="/" :event="password.length < 6 ? '' : 'click'">
                    <el-button 
                        :disabled="password.length < 6"
                        class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                        Sign up
                    </el-button>
                </NuxtLink>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    layout: 'noFooter',
    data() {
        return {
            email: '',
            password: '',
            promotions: false,
            isStepTwo: false,
        }
    },
};
</script>

<style>
</style>