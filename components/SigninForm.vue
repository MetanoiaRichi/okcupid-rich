<template>
    <el-dialog
        append-to-body
        :visible.sync="signInDialogVisible"
        :close-on-click-modal="false"
        @closed="closeDialog()"
        :close-on-press-escape="false">

        <section v-show="forgotPassword">
            <div
                @click="resetValues()"
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 left-5">
                <i class="el-icon-arrow-left go_back text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)] text-center">
                Enter your email to reset your password
            </h1>

            <el-form
                class="mb-8" 
                :model="resetEmailForm"
                :rules="resetEmailFormRule"
                @submit.native.prevent
                ref="resetEmailForm">
                <el-form-item label="Email" prop="email" required>
                    <el-input type="text" v-model="resetEmailForm.email" placeholder="Email"></el-input>
                </el-form-item>
            </el-form>

            <el-button 
                :disabled="resetEmailForm.email.trim() == ''"
                @click="submitForm('resetEmailForm')"
                class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                Reset Password
            </el-button>
        </section>

        <section v-show="loginWithPhone">
            <div
                @click="resetValues()" 
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 left-5">
                <i class="el-icon-arrow-left go_back text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)] text-center">
                What’s your phone number?
            </h1>

            <el-form
                class="mb-8"
                @submit.native.prevent>
                <el-form-item prop="phone">
                    <vue-tel-input v-model="loginWithPhoneForm.phone"></vue-tel-input>
                </el-form-item>
            </el-form>

            <p class=" text-xs text-gray-500 mb-8 text-center">
                We will send a text with a verification code. Message and data rates may apply. 
                <a class="underline" href="https://help.okcupid.com/article/202-sms-verification" target="_blank" rel="noopener noreferrer">Learn what happens when your number changes.</a>
            </p>

            <el-button 
                :disabled="!loginWithPhoneForm.phone"
                @click="resetValues()"
                class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                Next
            </el-button>
        </section>

        <section v-show="!forgotPassword && !loginWithPhone">
            <div
                @click="closeDialog()" 
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 right-5">
                <i class="el-icon-close text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)]">Enter email and password</h1>

            <el-form
                class="mb-8" 
                :model="loginForm"
                :rules="loginFormFormRules"
                @submit.native.prevent
                ref="loginForm">
                <el-form-item label="Email" prop="email" required>
                    <el-input type="text" v-model="loginForm.email" placeholder="Email"></el-input>
                </el-form-item>

                <el-form-item label="Password" prop="password" required>
                    <el-input type="password" v-model="loginForm.password" placeholder="Password"></el-input>
                </el-form-item>
            </el-form>

            <el-button 
                @click="submitForm('loginForm')"
                :disabled="loginForm.email.trim() == '' || loginForm.password.trim() == ''"
                class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white mb-6 uppercase" type="primary">
                Next
            </el-button>

            <label @click="forgotPassword = true" class="block text-sm font-semibold uppercase cursor-pointer text-center text-[color:var(--blue)]">Forgot Password?</label>

            <div class="or_container text-lg text-[color:var(--black)] flex items-center py-5">
                <span class="flex-1 h-[1px] bg-[#949aa6]"></span>
                <span class="shrink-0 px-4">or</span>
                <span class="flex-1 h-[1px] bg-[#949aa6]"></span>
            </div>

            <el-button 
                class="font-semibold tracking-[1px] text-base h-16 w-full text-white uppercase"
                @click="loginWithPhone = true" 
                type="primary">
                Log in with phone
            </el-button>
        </section>
    </el-dialog>
</template>

<script>
import { VueTelInput } from 'vue-tel-input';
import 'vue-tel-input/dist/vue-tel-input.css';

export default {
    props: {
        signInDialogVisible: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    components: {
        VueTelInput,
    },
    data() {
        return {
            forgotPassword: false,
            loginWithPhone: false,
            resetEmailForm: {
				email: '',
			},
            loginForm: {
				email: '',
                password: '',
			},
            loginWithPhoneForm: {
                phone: '',
			},
            resetEmailFormRule: {
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
            loginFormFormRules: {
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
            },
        }
    },
    methods: {
        closeDialog() {
            this.resetValues()
            this.$emit('close-dialog');
        },

        resetValues() {
            this.resetEmailForm = {
				email: '',
			}

            this.loginForm = {
				email: '',
                password: '',
			}

            this.loginWithPhoneForm = {
                phone: '',
			}

            this.forgotPassword = false;
            this.loginWithPhone = false;
        },

		submitForm(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    if(formName == 'loginForm') {
                        this.closeDialog()
                    } else {
                        this.resetValues()
                    }
                } else {
                    return false;
                }
            });
		},
	},
}
</script>