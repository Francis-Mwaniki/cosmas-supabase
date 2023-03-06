<template>    
 <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8 bg-slate-900">
 
      <div class="mx-auto max-w-lg">
      <h1 class=" items-center justify-center flex  text-4xl m-7 text-white">Log In</h1>
      <!-- Error alert  -->
      <div
          class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative"
          role="alert"
          v-show="success"
        >
          {{ success }} created!
        </div>
        <!-- warning alert -->
        <div
          class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
          role="alert"
          v-show="err"
        >
          {{ err }}!
        </div>
     
      <form
            action=""
            class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl bg-slate-800 text-white"
            @submit.prevent="handleSubmit"
          >
            <p class="text-lg font-medium">Welcome Back</p>
  
            <div>
              <label for="email" class="text-sm font-medium">Email</label>
  
              <div class="relative mt-1">
                <input
                  type="email"
                  id="email"
                  v-model="email"
                  class="w-full rounded-lg ring bg-slate-100 p-4 pr-12 text-sm shadow-sm"
                  placeholder="Enter email"
                />
   
              </div>
            </div>
            <div>
              <label for="password" class="text-sm font-medium">Password</label>
  
              <div class="relative mt-1">
                <input
                  type="password"
                  id="password"
                  v-model="password"
                  class="w-full rounded-lg ring bg-slate-100 p-4 pr-12 text-sm shadow-sm"
                  placeholder="Enter password"
                />
   
              </div>
            </div>
  
           
  
            <button
              type="submit"
              class="block w-full rounded-lg px-5 py-3 text-sm font-medium text-white"
                :class="loading? 'bg-gray-500' : 'bg-blue-500'"
            
              :disabled="loading"
            >
              {{ loading ? "Loading..." : "Sign Up" }}
            </button>
  
            <p class="text-center text-sm text-white">
              Don't Have an account?
              <NuxtLink to="/" class="underline">Sign Up</NuxtLink>
            </p>
          </form>
    </div>
  </div>
  </template>
  
  <script>
  import { createClient } from '@supabase/supabase-js';
  
export default {
  
  data() {
    return {
      email: "",
      name: "",
      loading: false,
      password: "",
      success: "",
      err: "",
       
    };
  },
  components: {},
  methods: {
    async handleSubmit() {
      const supabase = createClient(
       'https://swocaqwllmwkocyhqnhm.supabase.co',
       'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InN3b2NhcXdsbG13a29jeWhxbmhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NzExNzM2NDIsImV4cCI6MTk4Njc0OTY0Mn0.eE7E7QeAT2iGCsInhiPVjYqOEuyrfD0-OAKsKhuWVaI',
         );
      if (this.password.length < 8) {
        alert("Password must be at least 8 characters long");
        return;
      }
      const { data, error } = await supabase.auth.signInWithPassword({
        email: this.email,
        password: this.password,
      });
      if (error) {
        this.err = error.message;
        this.loading = false;
        console.log(error.message);
      } else {
        this.user = data.user.email;
        this.success = data.user.email;
        setTimeout(() => {
          this.$router.push("/products");
          this.loading = false;
        }, 2000);
        //this.$router.push("/Login");
      }
    },
  },
};
</script>