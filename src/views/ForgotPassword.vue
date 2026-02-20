
<template>
  <div class="login login-action-login">
    <div id="login">
      <h1 role="presentation" class="wp-login-logo">
        <img src="../assets/logo_main.svg" />
      </h1>

      <h2 class="t-lspace bold">
        កម្មវិធីបរិវត្តកម្មឌីជីថលទីស្តីការគណៈរដ្ឋមន្ត្រី
      </h2>

      <!-- Forgot Password Form -->
      <form @submit.prevent="handleRequestReset">
        <div class="input-wrapper mb-15">
          <input
            id="user_identifier"
            class="input form-control"
            v-model="identifier"
            type="text"
            autocomplete="off"
            placeholder="អ៊ីមែល ឬ លេខទូរស័ព្ទ"
            required
          />
          <div class="prefix">
            <!-- mail/phone icon -->
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.6" stroke="currentColor" aria-hidden="true" class="size-5 transition-colors duration-200"><path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75"></path></svg>
          </div>
        </div>
        <button type="submit" class="button button-primary button-large w-full mt-2">
          ស្នើសុំលេខកូដ 
        </button>
        <div><br></div>
      </form>
        <!-- Show VerifyCode page/component after request -->
        <!-- <div v-if="showVerifyCode" class="mt-6">
          <input
            id="otp"
            class="input form-control text-center tracking-widest text-lg"
            v-model="otp"
            type="text"
            maxlength="6"
            pattern="[0-9]{6}"
            autocomplete="one-time-code"
            placeholder="បញ្ចូលលេខកូដ ៦ ខ្ទង់"
            required
          />
          <br>
          <button class="button button-primary button-large w-full mt-2" @click="handleVerifyOtp">ផ្ញើលេខកូដ</button>
          <div v-if="otpMessage" class="mt-2 text-center text-red-600">{{ otpMessage }}</div>
        </div> -->
      <!-- OTP Modal Popup -->
      <div v-if="showVerifyCode" class="fixed inset-0 z-50 flex items-center justify-center" style="background: rgba(0,0,0,0.2);">
        <div class="bg-white rounded-lg shadow-lg p-8 relative w-full max-w-xs flex flex-col items-center">
          <button @click="closeOtpModal" class="absolute top-2 right-2 text-gray-400 hover:text-red-500 text-xl font-bold">×</button>
          <div class="mb-4 text-center font-semibold">បញ្ចូលលេខកូដ ៦ ខ្ទង់</div>
          <input
            id="otp"
            class="input form-control text-center tracking-widest text-lg mb-2"
            v-model="otp"
            type="text"
            maxlength="6"
            pattern="[0-9]{6}"
            autocomplete="one-time-code"
            placeholder="------"
            required
          />
          <button class="button button-primary button-large w-full mt-2" @click="handleVerifyOtp">ផ្ញើលេខកូដ</button>
          <div v-if="otpMessage" class="mt-2 text-center text-red-600">{{ otpMessage }}</div>
        </div>
      </div>
      <div v-if="message" class="mt-4 text-green-600 text-center">{{ message }}</div>
      <div class="mt-4 text-right hover:underline">
        <router-link to="/login" class="text-blue-500 hover:underline">ត្រឡប់ទៅទំព័រចូល</router-link>
      </div>
    </div>
  </div>

  <footer class="ocm_footer login_ac">
    រក្សាសិទ្ធិគ្រប់យ៉ាងដោយទីស្តីការគណៈរដ្ឋមន្ត្រី
  </footer>
</template>


<!-- <script>
import { ref } from "vue"

export default {
  name: "ForgotPassword",
  setup() {
    const identifier = ref("")
    const message = ref("")

    const handleRequestReset = () => {
      // TODO: Replace with real API call
      message.value = "ប្រសិនបើអ៊ីមែល ឬ លេខទូរស័ព្ទមានសុពលភាព អ្នកនឹងទទួលបានការណែនាំតាមអ៊ីមែល ឬ សារ។"
    }

    return {
      identifier,
      message,
      handleRequestReset
    }
  }
}
</script> -->


<script>
import { ref } from "vue"

export default {
  name: "ForgotPassword",
  setup() {
    const identifier = ref("")
    const message = ref("")
    const showVerifyCode = ref(false)
    const otp = ref("")
    const otpMessage = ref("")
    const handleVerifyOtp = () => {
      if (otp.value.length !== 6 || !/^[0-9]{6}$/.test(otp.value)) {
        otpMessage.value = "លេខកូដមិនត្រឹមត្រូវទេ។"
        return
      }
      otpMessage.value = "កូដត្រឹមត្រូវ"
    }
      const closeOtpModal = () => {
        showVerifyCode.value = false
        otp.value = ""
        otpMessage.value = ""
      }

    const handleRequestReset = () => {
      // Instantly show VerifyCode below, no backend check
      showVerifyCode.value = true
    }

    return {
      identifier,
      message,
      handleRequestReset,
      showVerifyCode,
      otp,
      otpMessage,
      handleVerifyOtp,
        closeOtpModal
    }
  }
}
</script>


<style scoped>
</style>
