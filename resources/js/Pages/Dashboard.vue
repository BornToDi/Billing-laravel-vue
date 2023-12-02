<template>

    <div class="bg-slate-50   rounded-lg border-yellow-300 container mx-auto md:mt-10">

        <div class=" bg-gradient-to-r from-blue-600 to-blue-400 rounded-full w-52 mx-auto text-center text-white text-bold py-2 my-6">Submit your form</div>

      <!---->
      <form class="" @submit.prevent="submitForm">
    <div v-for="(formData, index) in formDatas" :key="index" >
        <div class="border-2 border-slate-400 rounded-lg pt-10">

        <div class="grid grid-cols-1 lg:grid-cols-8 pb-5 ">

       <div class="px-2">
        <div class="text-center text-lg text-blue-600  ">From</div>
       <input v-model="formData.field1" type="text" class=" w-full border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-300">
      </div>

      <div class="px-2" >
        <div class="text-center text-lg text-blue-600  ">To</div>
        <input v-model="formData.field2" type="text" class=" w-full border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-300">
      </div>

      <div class="px-2">
            <div class="text-center text-lg text-blue-600">Vehicle</div>
            <select v-model="formData.vehicle" @change="updateFixedCost(index)" class="w-full border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-300">
              <option value="bus">Bus</option>
              <option value="bike">Bike</option>
              <option value="metro">Metro</option>
              <option value="cng">CNG</option>
            </select>
          </div>
          <div class="px-2">
            <div class="text-center text-lg text-blue-600">Fixed cost</div>
            <input v-model="formData.fixedCost" type="text" class="w-full border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-300">
          </div>

        <div class="px-2">
             <div class="text-center text-lg text-blue-600">Cost</div>
             <div class="relative">
    <input
        v-model="formData.cost"
        :class="{ 'bg-green-200': formData.fixedCost === formData.cost, 'bg-red-200': formData.fixedCost !== formData.cost }"
        type="text"
        class="w-full border border-gray-300 rounded-md pr-10 focus:outline-none focus:ring focus:border-blue-300"
    >

    <!-- Checkbox -->
    <div class="absolute inset-y-0 right-0 flex items-center pr-2">
        <input
            v-model="formData.checkboxValue"
            type="checkbox"
            :checked="formData.fixedCost === formData.cost"
            :class="{ 'bg-green-500': formData.fixedCost === formData.cost, 'bg-red-500': formData.fixedCost !== formData.cost }"
            class="rounded-xl"
        >
    </div>
</div>


        </div>

  <div class="px-2">
    <div class="text-center text-lg text-blue-600">File Upload</div>
    <div class="flex justify-center items-center">
      <label for="file-input" class=" bg-gradient-to-r from-blue-500 to-blue-300 relative cursor-pointer  text-white font-bold py-2 px-14 rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
        <svg class="absolute left-0 top-0 m-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="24" height="24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path>
        </svg>
        File
      </label>
      <input id="file-input" type="file" class="hidden " @change="handleFileChange($event, index)">

    </div>
  </div>

      <div class="px-2" >
        <div class="text-center text-lg text-blue-600  ">Describe</div>
        <input v-model="formData.field7" type="text" class=" w-full border border-gray-300 rounded-md focus:outline-none focus:ring focus:border-blue-300">
      </div>

      <div class="px-2 ">
    <div class="text-center text-lg text-blue-600">Remove</div>
    <button @click="removeItem(index)" class="container mx-auto py-2 rounded-lg bg-red-100 transition-all duration-300 hover:bg-red-300 text-red-500">❌</button>

</div>
      <!-- Repeat the structure for other fields -->
    </div>

        </div>

    </div>
    <div class="flex items-center pt-5">
    <button class="mx-auto px-8 mb-5 bg-blue-500 hover:bg-gradient-to-r from-blue-600 to-blue-400 text-white font-bold py-2  rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800" type="submit">Submit</button>
    </div>
    </form>
    </div>

    <div class="flex items-center pt-5 ">
      <button @click.prevent="addMore" class="bg-gradient-to-r from-blue-600 to-blue-400 mx-auto px-20 my-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2  rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
        Add More
      </button>
      </div>



  </template>

  <script>
  export default {
    data() {
      return {
        formDatas: [
          {
            field1: '',
            field2: '',
            fixedCost: '',
            cost: '',
            field7: '',
            file: '',
            checkboxValue: false,
          }
        ],
      };
    },
    methods: {
        handleFileChange(event, index) {
  const selectedFile = event.target.files[0];

  if (selectedFile) {
    // Update the file property of the specific form instance
    this.formDatas[index].file = selectedFile;

    // Log the entire form data including the file
    console.log(`Form data for form ${index + 1} with file:`, this.formDatas);
  } else {
    console.log('No file selected');
  }
},

submitForm() {
  // Handle form submission here
  console.log('Form submitted with data:', this.formDatas);

  // Reset input values after form submission
  this.formDatas = [
    {
      field1: '',
      field2: '',
      fixedCost: '',
      cost: '',
      field7: '',
      file: '',
      checkboxValue: false,
    }
  ];
},
      addMore() {
        // Add a new empty form data set
        this.formDatas.push({
            field1: '',
            field2: '',
            fixedCost: '',
            cost: '',
            field7: '',
            file: '',
        });
      },
       updateFixedCost(index) {
      const vehicle = this.formDatas[index].vehicle;
      // Set the fixed cost based on the selected vehicle
      this.formDatas[index].fixedCost = this.calculateFixedCost(vehicle);
    },
    calculateFixedCost(vehicle) {
      // Add your logic to calculate fixed cost based on the selected vehicle
      switch (vehicle) {
        case 'bus':
          return '20';
          case 'bike':
          return '100';
          case 'cng':
          return '200';
        case 'metro':
          return '40';
        // Add more cases for other vehicles
        default:
          return '';
      }
    },
    removeItem(index) {
        // Implement the logic to remove the form data at the specified index
        this.formDatas.splice(index, 1);
    },
    },
  };
  </script>

  <style scoped>
  /* Add any component-specific styles here */
  </style>
