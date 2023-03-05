<template>
    <div>
        <div class="flex justify-center items-center min-h-screen bg-slate-900">
  <div class="w-full max-w-md p-6 bg-white rounded-lg dark:text-white text-black shadow-md dark:bg-slate-800">
    <h2 class="text-lg font-bold mb-4">Contact Us</h2>
    <form class=" text-white">
      <div class="mb-4">
        <label for="name" class="block dark:text-white text-gray-700 font-bold mb-2">Name</label>
        <input type="text" id="name" name="name" class="form-input w-full py-2" placeholder="Enter your name">
      </div>
      <div class="mb-4">
        <label for="email" class="block dark:text-white text-gray-700 font-bold mb-2">Email</label>
        <input type="email" id="email" name="email" class="form-input w-full py-2" placeholder="Enter your email">
      </div>
      <div class="mb-4">
        <label for="message" class="block dark:text-white text-gray-700 font-bold mb-2">Message</label>
        <textarea id="message" name="message" class="form-textarea w-full" rows="5" placeholder="Enter your message"></textarea>
      </div>
      <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">Submit</button>
    </form>
  </div>
</div>

    </div>
</template>

<script>
    export default {
        
    }
</script>

<style  scoped>

</style>