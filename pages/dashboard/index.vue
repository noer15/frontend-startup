<template>
  <div>
    <section class="container mx-auto pt-8">
      <div class="flex justify-between items-center mb-6">
        <div class="w-3/4 mr-6">
          <h2 class="text-4xl text-gray-900 mb-2 font-medium">Dashboard</h2>
          <ul class="flex mt-2">
            <li class="mr-6">
              <a class="text-gray-800 font-bold" href="#"> Your Projects </a>
            </li>
            <li class="mr-6">
              <NuxtLink
                class="text-gray-500 hover:text-gray-800"
                to="/dashboard/transactions"
              >
                Your Transactions
              </NuxtLink>
            </li>
          </ul>
        </div>
        <div class="w-1/4 text-right">
          <NuxtLink
            to="/dashboard/projects/create"
            class="bg-orange-button hover:bg-green-button text-white font-bold py-4 px-4 rounded inline-flex items-center"
          >
            + Create Campaign
          </NuxtLink>
        </div>
      </div>
      <hr />
      <div class="block mb-2">
        <div
          v-for="campaign in dashboard.data"
          :key="campaign.id"
          class="w-full lg:max-w-full lg:flex mb-4"
        >
          <div
            class="h-48 lg:h-auto lg:w-48 flex-none bg-cover rounded-t lg:rounded-t-none lg:rounded-l text-center overflow-hidden"
            :style="
              'background-color: gray; background-position: center; background-image: url(\'' +
              $axios.defaults.baseURL +
              '/' +
              campaign.image_url +
              '\')'
            "
          ></div>
          <NuxtLink
            :to="'dashboard/projects/' + campaign.id"
            class="w-full border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-8 flex flex-col justify-between leading-normal"
          >
            <div class="mb-8">
              <div class="text-gray-900 font-bold text-xl mb-1">
                {{ campaign.name }}
              </div>
              <p class="text-sm text-gray-600 flex items-center mb-2">
                Rp.
                {{ new Intl.NumberFormat().format(campaign.goal_amount) }}
                &middot;
                {{ (campaign.goal_amount / campaign.current_amount) * 100 }}%%
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.short_description }}
              </p>
            </div>
            <div class="flex items-center">
              <NuxtLink
                :to="'/dashboard/detail/' + campaign.id"
                class="bg-green-button text-white py-2 px-4 rounded"
              >
                Detail
              </NuxtLink>
            </div>
          </NuxtLink>
        </div>
      </div>
    </section>
    <div class="cta-clip -mt-20"></div>
  </div>
</template>
<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios, app }) {
    const dashboard = await $axios.$get(
      '/api/v1/campaigns?user_id=' + app.$auth.user.id
    )
    return { dashboard }
  },
}
</script>
