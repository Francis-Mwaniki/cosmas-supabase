<template>
    <main class="  bg-slate-500 items-center justify-center flex ">
    <div class="">
    <h1 class=" text-yellow-400 m-6">MANAGE YOUR WINDOW SHOPPING </h1>
    <div class=" bg-slate-900 text-white items-center justify-center flex flex-col rounded-lg">
    
      <form @submit.prevent="addProduct" class="  items-center justify-center flex flex-col">
        <label for="">Enter new product</label>
        <input type="text" placeholder=" product name" v-model="newProduct.name" class=" rounded-md p-3 m-4 text-black" required />
        <label for="">Price</label>
        <input type="number" placeholder="price" v-model="newProduct.price" class=" rounded-md p-3 m-4 text-black" />
        <button type="submit" class=" bg-blue-700 p-3 rounded-md mb-4 hover:scale-75">add product</button>
      </form> 
      <button @click="deleteProduct(product.id)">Delete</button>

       <ul class=" text-white p-3 rounded-md">
        <li v-for="product in products" :key="product.id">
          {{ product.name }} - ksh{{ product.price }}         </li>
      </ul>
    </div>
</div></main>
  </template>
  
  <script>
  import { createClient } from "@supabase/supabase-js";
  
  const supabase = createClient(
    "https://swocaqwllmwkocyhqnhm.supabase.co",
    "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InN3b2NhcXdsbG13a29jeWhxbmhtIiwicm9sZSI6ImFub24iLCJpYXQiOjE2NzExNzM2NDIsImV4cCI6MTk4Njc0OTY0Mn0.eE7E7QeAT2iGCsInhiPVjYqOEuyrfD0-OAKsKhuWVaI"
  );
  
  export default {
    data() {
      return {
        products: [ ],
        newProduct: { name: "", price: 0 },
      };
    },
    async created() {
      // Fetch the products from Supabase and set them in the products array
      const { data } = await supabase.from("products").select("*");
      this.products = data;
    },
    methods: {
      async addProduct() {
        const { data, error } = await supabase
          .from("products")
          .insert(this.newProduct);
  
        if (error) {
          alert(error.message);
        } else {
          // Add the new product to the products array
          this.products.push(data[0]);
      
          this.newProduct.name = "";
          this.newProduct.price = 0;
        }
        if(this.product.length>1){
          this.err='place something here'
          return
        } 
      },
      async deleteProduct(id) {
      const { error } = await supabase.from("products").delete().match({ id });
      if (error) {
        alert(error.message);
      } else {
        this.products = this.products.filter(product => product.id !== id);
      }
    }
    },
  };
  </script>
  