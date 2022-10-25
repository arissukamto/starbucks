<template>
  <!-- <div class="max-w-screen-sm mx-auto px-4 py-10"> -->
    <!-- Error Handling -->
    <!-- <div v-if="errorMsg" class="mb-10 p-4 rounded-md bg-light-grey shadow-lg">
      <p class="text-red-500">{{ errorMsg }}</p>
    </div> -->

    
    <!-- Container -->
<div class="flex flex-wrap min-h-screen w-full content-center justify-center bg-gray-200 py-10">
  
  <!-- Login component -->
  <div class="flex shadow-md">
      <!-- Login banner -->
    <div class="flex flex-wrap content-center justify-center rounded-r-md" style="width: 24rem; height: 32rem;">
      <img class="w-full h-full bg-center bg-no-repeat bg-cover rounded-r-md" src="../assets/images/login.png">
    </div>
    <!-- Login form -->
    <div class="flex flex-wrap content-center justify-center rounded-l-md bg-white" style="width: 24rem; height: 32rem;">
      <div class="w-72">
        <!-- Heading -->
        <h1 class="text-xl font-semibold text-center">Login</h1>
        <!-- Form -->
        <form class="mt-4">
          <div class="mb-3">
            <label class="email-input mb-2 block text-xs font-reguler">Email</label>
            <input type="email" placeholder="Enter your email" class="block w-full rounded-md border bg-gray-200 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500" />
          </div>

          <div class="mb-3">
            <label class="password-input mb-2 block text-xs font-semibold">Password</label>
            <input type="password" placeholder="*****" class="block w-full rounded-md border bg-gray-200 focus:border-purple-700 focus:outline-none focus:ring-1 focus:ring-purple-700 py-1 px-1.5 text-gray-500" />
          </div>

          <div class="mb-3">
            <button class="login-btn mb-1.5 block w-full text-center text-white bg-green-700 hover:bg-yellow-900 px-2 py-1.5 rounded-md">Sign in</button>
          </div>
        </form>

        <!-- Footer -->
        <div class="text-center">
          <router-link class="text-sm mt-6 text-center" :to="{ name: 'Register' }">
            Don't have an account? <span class="text-at-light-green">Register</span>
           </router-link>
        </div>
      </div>
    </div>

  
  </div>
</div>

    <!-- Login -->
    <!-- <form
      @submit.prevent="login"
      class="p-8 flex flex-col bg-light-grey rounded-md shadow-lg"
    >
      <h1 class="text-3xl text-at-light-black mb-4 text-center">Login</h1>

      <div class="flex flex-col mb-2">
        <label for="email" class="mb-1 text-sm text-at-light-black">Email</label>
        <input
          type="text"
          required
          class="p-2 text-gray-500 focus:outline-none"
          id="email"
          v-model="email"
        />
      </div>

      <div class="flex flex-col mb-2">
        <label for="password" class="mb-1 text-sm text-at-light-black">Password</label>
        <input
          type="password"
          required
          class="p-2 text-gray-500 focus:outline-none"
          id="password"
          v-model="password"
        />
      </div>

      <button
        type="submit"
        class="mt-6 py-2 px-6 rounded-sm self-start text-sm
      text-white bg-at-light-green duration-200 border-solid
      border-2 border-transparent hover:border-at-light-green hover:bg-white
      hover:text-at-light-green"
      >
        Login
      </button>

      <router-link class="text-sm mt-6 text-center" :to="{ name: 'Register' }">
        Don't have an account? <span class="text-at-light-green">Register</span>
      </router-link>
    </form> -->
  <!-- </div> -->
</template>

<script>
import { ref } from "vue";
import { supabase } from "../supabase/init";
import { useRouter } from "vue-router";

export default {
  name: "login",
  setup() {
    // Create data / vars
    const router = useRouter();
    const email = ref(null);
    const password = ref(null);
    const errorMsg = ref(null);

    // Login function
    const login = async () => {
      try {
        const { error } = await supabase.auth.signIn({
          email: email.value,
          password: password.value,
        });
        if (error) throw error;
        router.push({ name: "Home" });
      } catch (error) {
        errorMsg.value = `Error: ${error.message}`;
        setTimeout(() => {
          errorMsg.value = null;
        }, 5000);
      }
    };

    return { email, password, errorMsg, login };
  },
};
</script>
