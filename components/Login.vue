<template>
  <section class="py-6">
    <div class="container mx-auto">
      <div class="w-full max-w-sm mx-auto">
       
        <h2 class="text-slate-600 font-bold text-3xl text-center mb-6">Welcome</h2>


        <Notification :message="error" v-if="error" />

        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" method="post" @submit.prevent="login">
          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2" for="email">
              Email
            </label>
            <input
              type="email"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="email"
              name="email"
              v-model="email"
              placeholder="Email Address"
            />
          </div>
          <div class="mb-6">
            <label class="block text-gray-700 font-bold mb-2" for="password">
              Password
            </label>
            <input
              type="password"
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="password"
              name="password"
              v-model="password"
              placeholder="Password"
            />
          </div>
          <div class="flex items-center justify-between">
            <button type="submit" class="bg-gray-900 hover:bg-gray-800 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" :disabled="!isValid">
              Log In
            </button>
          </div>
        </form>
        <div class="text-center">
          <p class="text-sm">
            Forgot your Password? <nuxt-link to="/reset" class="font-bold text-gray-700">Reset</nuxt-link>
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Login',
};
</script>
