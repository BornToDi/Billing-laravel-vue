<!-- billing-form.vue -->

<template>
    <div class="bg-gray-200 min-h-screen flex items-center justify-center">
      <div class="bg-white p-8 rounded shadow-md w-96">
        <h1 class="text-2xl font-bold mb-6">Employee Billing Form</h1>

        <form @submit.prevent="submitForm">
          <!-- Employee Information -->
          <div class="mb-4">
            <label for="employeeName" class="block text-sm font-medium text-gray-600">Employee Name</label>
            <input v-model="employeeName" type="text" id="employeeName" name="employeeName" class="mt-1 p-2 w-full border rounded-md">
          </div>

          <!-- Billing Details -->
          <div class="mb-4">
            <label for="amount" class="block text-sm font-medium text-gray-600">Billing Amount</label>
            <input v-model="billingAmount" type="number" id="amount" name="amount" class="mt-1 p-2 w-full border rounded-md">
          </div>

          <!-- Submit Button -->
          <div class="flex justify-end">
            <button type="submit" class="bg-blue-500 text-white p-2 rounded-md">Submit</button>
          </div>
        </form>
      </div>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        employeeName: '',
        billingAmount: 0,
      };
    },
    methods: {
      submitForm() {
        // Handle form submission logic here
        console.log('Form submitted:', this.employeeName, this.billingAmount);
      },
    },
  };
  </script>

  <style scoped>
  /* Add your custom styles here or use Tailwind classes directly in the template */
  </style>
