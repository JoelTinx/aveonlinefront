<template>
  <div class="dark:bg-gray-900 app-container">
    <div class="container items-center mx-auto p-5">
      <div class="flex justify-between">
        <h1 class="text-2xl dark:text-white font-bold uppercase">Promotions</h1>
        <button
          v-if="!creating"
          type="button"
          class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:ring-blue-300 dark:focus:ring-blue-800 shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
          @click="creating = true"
        >
          Create
        </button>
      </div>

      <div v-if="creating">
        <form @submit.prevent="postPromotion">
          <div class="mb-6">
            <label
              for="description"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
              >Name</label
            >
            <input
              type="text"
              id="description"
              class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
              placeholder="Description"
              required
              v-model="promotion.description"
            />
          </div>
          <div class="mb-6">
            <label
              for="percentage"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
              >Percentage</label
            >
            <input
              id="percentage"
              type="number"
              class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
              placeholder="0.00"
              required
              v-model="promotion.percentage"
            />
          </div>
          <div class="mb-6">
            <label
              for="startdate"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
              >Start Date</label
            >
            <input
              id="startdate"
              type="date"
              class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
              required
              v-model="promotion.start_date"
            />
          </div>
          <div class="mb-6">
            <label
              for="enddate"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
              >End Date</label
            >
            <input
              id="enddate"
              type="date"
              class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
              required
              v-model="promotion.end_date"
            />
          </div>
          <div class="text-center">
            <button
              type="submit"
              class="text-white bg-gradient-to-r from-green-400 via-green-500 to-green-600 hover:bg-gradient-to-br focus:ring-4 focus:ring-green-300 dark:focus:ring-green-800 shadow-lg shadow-green-500/50 dark:shadow-lg dark:shadow-green-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
            >
              Save
            </button>
            <button
              class="relative inline-flex items-center justify-center p-0.5 mb-2 mr-2 overflow-hidden text-sm font-medium text-gray-900 rounded-lg group bg-gradient-to-br from-cyan-500 to-blue-500 group-hover:from-cyan-500 group-hover:to-blue-500 hover:text-white dark:text-white focus:ring-4 focus:ring-cyan-200 dark:focus:ring-cyan-800"
              @click="cancelCreation"
            >
              <span
                class="relative px-5 py-2.5 transition-all ease-in duration-75 bg-white dark:bg-gray-900 rounded-md group-hover:bg-opacity-0"
              >
                Cancel
              </span>
            </button>
          </div>
        </form>
      </div>

      <div class="flex flex-col" v-if="!creating">
        <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block py-2 min-w-full sm:px-6 lg:px-8">
            <div class="overflow-hidden shadow-md sm:rounded-lg">
              <table class="min-w-full">
                <thead class="bg-gray-50 dark:bg-gray-700">
                  <tr>
                    <th
                      scope="col"
                      class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400"
                    >
                      Id
                    </th>
                    <th
                      scope="col"
                      class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400"
                    >
                      Description
                    </th>
                    <th
                      scope="col"
                      class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400"
                    >
                      Start Date
                    </th>
                    <th
                      scope="col"
                      class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400"
                    >
                      End Date
                    </th>
                    <th
                      scope="col"
                      class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400"
                    >
                      Percentage
                    </th>
                    <th scope="col" class="relative py-3 px-6">
                      <span class="sr-only">Edit</span>
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr
                    class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:cursor-pointer"
                    v-for="pro in promotions"
                    v-bind:key="pro.id"
                  >
                    <td
                      class="py-4 px-6 text-sm text-gray-500 whitespace-nowrap dark:text-gray-400"
                    >
                      {{ pro.id }}
                    </td>
                    <td
                      class="py-4 px-6 text-sm font-medium text-gray-900 whitespace-nowrap dark:text-white"
                    >
                      {{ uppercase(pro.description) }}
                    </td>
                    <td
                      class="py-4 px-6 text-sm text-gray-500 whitespace-nowrap dark:text-gray-400"
                    >
                      {{ formatDate(pro.start_date) }}
                    </td>
                    <td
                      class="py-4 px-6 text-sm text-gray-500 whitespace-nowrap dark:text-gray-400"
                    >
                      {{ formatDate(pro.end_date) }}
                    </td>
                    <td
                      class="py-4 px-6 text-sm text-gray-500 whitespace-nowrap dark:text-gray-400"
                    >
                      {{ pro.percentage }}%
                    </td>
                    <td
                      class="py-4 px-6 text-sm font-medium text-right whitespace-nowrap"
                    >
                      <a
                        href="#"
                        class="text-blue-600 dark:text-blue-500 hover:underline"
                        >Edit</a
                      >
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as daysjs from "dayjs";

export default {
  data() {
    return {
      promotion: {
        description: "",
        performance: 10,
        start_date: "",
        end_date: "",
      },
      promotions: [],
      creating: false,
    };
  },
  created() {
    this.getPromotions();
  },
  computed: {
    uppercase() {
      return (v) => v.toUpperCase();
    },
    formatDate() {
      return (d) => daysjs(d).format("YYYY-MM-DD");
    },
  },
  methods: {
    getPromotions: function () {
      const me = this;
      fetch("http://127.0.0.1:5000/api/promotions")
        .then((res) => res.json())
        .then((res) => {
          me.promotions = res;
        });
    },
    postPromotion: function () {
      const me = this;
      fetch("http://127.0.0.1:5000/api/promotions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.promotion),
      })
        .then((res) => res.json())
        .then(() => {
          me.resetPromotion();
          me.showForm(false);
          me.getPromotions();
        });
    },
    resetPromotion: function () {
      this.promotion = {
        description: "",
        performance: 10,
        start_date: "",
        end_date: "",
      };
    },
    showForm: function (show = true) {
      const me = this;
      me.creating = show;
    },
    cancelCreation: function () {
      const me = this;
      me.resetPromotion();
      me.showForm(false);
    },
  },
};
</script>

<style scoped>
.app-container {
  min-height: calc(100vh - 60px);
}
</style>
