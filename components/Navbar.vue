<template>
  <nav class="bg-gray-800">
    <div class="container mx-auto px-6 py-3">
      <div class="flex items-center justify-between">
        <div class="hidden md:block">
          <nuxt-link class="navbar-item bg-gray-100 hover:bg-gray-800 text-slate-500 font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" to="/">Crocodile Solutions INC</nuxt-link>
        </div>
        <div class="flex items-center">
          <button class="flex md:hidden text-gray-500 hover:text-white focus:outline-none focus:text-white">
            <svg class="h-6 w-6 fill-current text-white" viewBox="0 0 24 24">
              <path v-if="!open" fill-rule="evenodd" clip-rule="evenodd" d="M4 6h16V8H4V6ZM4 11h16v2H4v-2ZM4 16h16v2H4v-2Z"></path>
              <path v-else fill-rule="evenodd" clip-rule="evenodd" d="M6.343 4.343L7.757 2.93l9.9 9.9-9.9 9.9-1.414-1.414 8.486-8.486L6.343 4.343z"></path>
            </svg>
          </button>
        </div>
      </div>
      </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      open: false
    };
  }
};
</script>
