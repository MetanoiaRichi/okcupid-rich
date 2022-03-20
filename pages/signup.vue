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

                <el-form 
                    class="mb-28" 
                    :model="emailForm"
                    :rules="emailFormRule"
                    @submit.native.prevent
                    ref="emailForm">

                    <el-form-item label="Email" prop="email" required>
                        <el-input type="text" v-model="emailForm.email" placeholder="Email"></el-input>
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
                    :disabled="emailForm.email.trim() == ''"
                    @click="submitForm('emailForm')"
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

                <el-form
                    class="mb-28" 
                    :model="passwordForm"
                    @submit.native.prevent
                    :rules="passwordFormRule"
                    ref="emailForm">
                    <el-form-item label="Password" prop="password" required>
                        <el-input type="password" v-model="passwordForm.password" placeholder="6 characters minimum"></el-input>
                    </el-form-item>
                </el-form>

                <el-button 
                    :disabled="passwordForm.password.length < 6"
                    @click="submitForm()"
                    class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                    Sign up
                </el-button>
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
            emailForm: {
				email: '',
			},
            emailFormRule: {
				email: [
                    {
						required: true,
						message: "Please input an email",
						trigger: "blur",
					},
					{
                        pattern: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
						message: "Please input a valid email",
						trigger: "blur",
					},
				],
            },
            passwordForm: {
				password: '',
			},
            passwordFormRule: {
				password: [
                    {
						required: true,
						message: "Please input a password",
                        trigger: "blur",
                    },
                    {
						min: 6,
						message: "Password length should at least be 6",
                        trigger: "blur",
                    },
				],
            }
        }
    },
    methods: {
		submitForm(formName) {
            if(formName) {
                this.$refs[formName].validate((valid) => {
                    if (valid) {
                        this.isStepTwo = true;
                    } else {
                        return false;
                    }
                });
            }
            else {
                this.$router.push('/');
            }
		},
	},
};
</script>

<style>
</style>