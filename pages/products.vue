<template>
  <main class="bg-slate-900 items-center justify-center flex">
    <div class="">

      <h1 class="text-yellow-400 m-6 justify-center items-center flex mx-auto text-3xl">
        MANAGE YOUR WINDOW SHOPPING
      </h1>
      <div
        class="bg-slate-900 text-white items-center justify-center flex flex-col rounded-lg my-1"
      >
        <div
          class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative w-full mx-auto"
          role="alert"
          v-show="success"
        >
          {{ success }} created!
        </div>
        <!-- warning alert -->
        <div
          class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative my-1 w-full mx-auto"
          role="alert"
          v-show="err"
        >
          {{ err }}!
        </div>
 

        <form
          @submit.prevent="addItemsToArray"
          class="items-center justify-center flex flex-col bg-slate-800 py-2 px-2"
        >
          <label for="">Enter new product</label>
          <input
            type="text"
            placeholder=" product name"
            v-model="newProduct.name"
            class="rounded-md p-3 m-4 text-black dark:text-white"
          />
          <label for="">Price</label>
          <!-- product description textarea -->
          <textarea
            name=""
            id=""
            cols="30"
            rows="10"
            placeholder="product description"
            v-model="newProduct.description"
            class="rounded-md p-3 m-4 text-black dark:text-white"
          ></textarea>
          <input
            type="number"
            placeholder="price"
            v-model="newProduct.price"
            class="rounded-md p-3 m-4 text-black dark:text-white"
          />
          <!-- product image -->
          <input
            type="text"
            placeholder="image url"
            v-model="newProduct.image"
            class="rounded-md p-3 m-4 text-black dark:text-white"
          />
          <button type="submit" class="bg-blue-700 p-3 rounded-md mb-4">
            add product
          </button>
        </form>

        <div
          class="bg-slate-900 text-white grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 grid-flow-row mx-auto items-center justify-center gap-2 my-5"
        >
          <div class="" v-for="product in items" :key="product">
            <div class="w-full bg-slate-700 rounded p-1">
              <img
                :src="product.image"
                alt="Product Image"
                class="rounded-lg shadow-lg object-cover w-full max-h-52"
              />
              <h2 class="text-lg font-bold mt-2">{{ product.name }}</h2>
              <p class="text-sm">{{ product.description }}</p>
              <p class="text-lg font-bold mt-2">${{ product.price }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
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
      items: [
        {
          id: 1,
          name: "product 1",
          description: "product 1 description",
          price: 100,
          image: "https://cdn.pixabay.com/photo/2017/11/22/22/53/nuts-2971675__340.jpg",
        },
        {
          id: 2,
          name: "product 2",
          description: "product 2 description",
          price: 200,
          image: "https://cdn.pixabay.com/photo/2018/02/01/19/21/easter-3123834__340.jpg",
        },
        {
          id: 3,
          name: "product 3",
          description: "product 3 description",
          price: 300,
          image:
            "https://cdn.pixabay.com/photo/2017/03/31/18/02/strawberry-dessert-2191973__340.jpg",
        },
        {
          id: 4,
          name: "product 4",
          description: "product 4 description",
          price: 400,
          image: "https://cdn.pixabay.com/photo/2021/01/05/05/30/grapes-5889697__340.jpg",
        },
      ],
      newProduct: { name: "", price: null, description: "", image: "" },
      name: "",
      image: "",
      description: "",
      price: null,
      success: "",
      err: "",
    };
  },
  async created() {
    // Fetch the products from Supabase and set them in the products array
    const { data } = await supabase.from("products").select("*");
    this.products = data;
  },
  methods: {
    /* Array to test */
    addItemsToArray() {
      if (
        !(
          this.newProduct.description &&
          this.newProduct.price &&
          this.newProduct.image &&
          this.newProduct.name
        )
      ) {
        this.err = "The product is empty";
      } else {
        this.items.push(this.newProduct);
        this.success = "Product added successfully";
        this.err = "";
        this.newProduct = { name: "", price: null, description: "", image: "" };
        setTimeout(() => {
          this.success = "";
          this.err = "";
        }, 3000);
      }
    },
    async addProduct() {
      const { data, error } = await supabase.from("products").insert(this.newProduct);

      if (error) {
        alert(error.message);
      } else {
        // Add the new product to the products array
        this.products.push(data[0]);
        // Clear the form inputs
        this.newProduct.name = "";
        this.newProduct.price = 0;
      }
    },
 
      const { error } = await supabase.from("products").delete().match({ id });
      if (error) {
        alert(error.message);
      } else {
        this.products = this.products.filter((product) => product.id !== id);
      }
    },
  },
};
</script>
