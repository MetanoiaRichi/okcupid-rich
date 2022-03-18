<template>
    <el-dialog
        append-to-body
        :visible.sync="signInDialogVisible"
        :close-on-click-modal="false"
        @closed="resetValues()"
        :close-on-press-escape="false">

        <template v-if="forgotPassword">
            <div
                @click="forgotPassword = false" 
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 left-5">
                <i class="el-icon-arrow-left go_back text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)] text-center">
                Enter your email to reset your password
            </h1>

            <el-form class="mb-8">
                <el-form-item label="Email" required>
                    <el-input type="text" v-model="email" placeholder="Email"></el-input>
                </el-form-item>
            </el-form>

            <el-button 
                :disabled="email.trim() == ''"
                @click="resetValues()"
                class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                Reset Password
            </el-button>
        </template>

        <template v-else-if="loginWithPhone">
            <div
                @click="loginWithPhone = false" 
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 left-5">
                <i class="el-icon-arrow-left go_back text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)] text-center">
                What’s your phone number?
            </h1>

            <el-form class="mb-8">
                <div class="flex items-center">
                    <el-form-item class="w-[90px] mb-0">
                        <el-select 
                            v-model="phonePrefix"
                            placeholder="Phone Prefix">
                            <el-option label="+63" :value="0">
                                Philippines +63
                            </el-option>
                        </el-select>
                    </el-form-item>

                    <el-form-item class="ml-5 flex-1 mb-0">
                        <el-input-number type="number" :min="0" :controls="false" v-model="phone" placeholder="Phone Number"></el-input-number>
                    </el-form-item>
                </div>
            </el-form>

            <p class=" text-xs text-gray-500 mb-8 text-center">
                We will send a text with a verification code. Message and data rates may apply. 
                <a class="underline" href="https://help.okcupid.com/article/202-sms-verification" target="_blank" rel="noopener noreferrer">Learn what happens when your number changes.</a>
            </p>

            <el-button 
                :disabled="!phone"
                @click="resetValues()"
                class="font-semibold tracking-[1px] w-full border-0 text-base h-16 text-white uppercase" type="primary">
                Next
            </el-button>
        </template>

        <template v-else>
            <div
                @click="resetValues()" 
                class="cursor-pointer text-[color:var(--blue)] absolute top-5 right-5">
                <i class="el-icon-close text-3xl"></i>
            </div>

            <h1 class="text-2xl mb-5 font-semibold text-[color:var(--gray)]">Enter email and password</h1>

            <el-form class="mb-8">
                <el-form-item label="Email" required>
                    <el-input type="text" v-model="email" placeholder="Email"></el-input>
                </el-form-item>

                <el-form-item label="Password" required>
                    <el-input type="password" v-model="password" placeholder="Password"></el-input>
                </el-form-item>
            </el-form>

            <el-button 
                @click="resetValues()"
                :disabled="email.trim() == '' || password.trim() == ''"
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
        </template>
    </el-dialog>
</template>

<script>
export default {
    props: {
        signInDialogVisible: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    data() {
        return {
            forgotPassword: false,
            loginWithPhone: false,
            email: '',
            password: '',
            phone: '',
            phonePrefix: 0,
        }
    },
    methods: {
        resetValues() {
            this.$emit('close-dialog');
            this.email = '';
            this.password = '';
            this.phone = '';
            this.forgotPassword = false;
            this.loginWithPhone = false;
        }
    }
}
</script>