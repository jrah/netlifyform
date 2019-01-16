<template>

  <form
    name="contact"
    method="post"
    netlify
    netlify-honeypot="bot-field"
    @submit.prevent="validateBeforeSubmit">
    <input
      type="hidden"
      name="form-name"
      value="contact" >
    <p style="display: none;">
      <label>Don’t fill this out: <input name="bot-field"></label>
    </p>

    <div class="column is-12">
      <label
        class="block text-blackbasic font-bold md:text-right mb-1 md:mb-0 pr-4"
        for="email">Name</label>
      <input
        v-validate="'required|max:60'"
        v-model="name"
        :class="{'input': true, 'border-red': errors.has('name') }"
        class="appearance-none block w-full bg-grey-lightest text-grey-darker border rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
        name="name"
        type="text"
        placeholder="Email">
      <span
        v-show="errors.has('name')"
        class="text-red text-xs italic">{{ errors.first('name') }}</span>
    </div>

    <div class="column is-12">
      <label
        class="block text-blackbasic font-bold md:text-right mb-1 md:mb-0 pr-4"
        for="email">Email</label>
      <input
        v-validate="'required|email'"
        v-model="email"
        :class="{'input': true, 'border-red': errors.has('email') }"
        class="appearance-none block w-full bg-grey-lightest text-grey-darker border rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
        name="email"
        type="text"
        placeholder="Email">
      <span
        v-show="errors.has('email')"
        class="text-red text-xs italic">{{ errors.first('email') }}</span>
    </div>



    <div class="column is-12">
      <label
        class="block text-blackbasic font-bold md:text-right mb-1 md:mb-0 pr-4"
        for="message">Message</label>
      <textarea
        v-validate="'required|max:360'"
        v-model="message"
        :class="{'input': true, 'border-red': errors.has('message') }"
        name="message"
        class="w-full h-32 bg-grey-lightest text-grey-darker border rounded py-3 px-4 mb-3 leading-tight focus:outline-none"
        style="vertical-align: top;"
        type="textarea"/>
      <span
        v-show="errors.has('message')"
        class="text-red text-xs italic">{{ errors.first('message') }}</span>
    </div>

    <div class="flex justify-end">
      <button
        class="inline-flex cursor-pointer bg-transparent hover:bg-point text-point-dark font-semibold hover:text-white py-2 px-4 border border-point hover:border-transparent rounded"
        type="submit">Submit</button>
    </div>

  </form>

</template>
<script>
import axios from "axios";
export default {
  name: "Contact",
  data: () => ({
    email: "",
    name: "",
    message: ""
  }),
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    validateBeforeSubmit() {
      const axiosConfig = {
        header: { "Content-Type": "application/x-www-form-urlencoded" }
      };
      axios.post(
        "/",
        this.encode({
          "form-name": "contact",
          ...this.form
        })
          .then(() => {
            alert("submitted");
          })
          .catch(() => {
            alert("failed");
          })
      );
    }
  }
};
</script>
