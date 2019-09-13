<template>
  <div class="container mx-auto pt-32">
    <h1 class=" text-center text-white font-semibold text-3xl">Start your podcast today:</h1>
    <div class="flex mt-12">
      <div class="w-1/2 flex flex-col items-end px-4">
        <div class="flex justify-center items-center w-108 px-4">
          <div 
          class="text-gray-600 px-2 py-1 bg-gray-800 rounded-lg uppercase text-xs font-bold cursor-pointer selector" 
          :class="{ 'cycleSelected' : billingCycle === 'monthly'}"
          @click="billingCycle = 'monthly'"
          >
            Monthly
          </div>
          <div 
          class="text-gray-600 px-2 py-1 bg-gray-800 rounded-lg uppercase text-xs font-bold cursor-pointer selector" 
          :class="{ 'cycleSelected' : billingCycle === 'yearly'}"
          @click="billingCycle = 'yearly'"
          >
            Yearly
          </div>
        </div>
        <div 
        v-for="sub in subscriptionTypes" 
        class="border-2 border-gray-800 w-108 mt-4 rounded-lg pl-6 pt-4 pb-4 flex cursor-pointer items-center hover:bg-gray-800 text-gray-500 hover:text-white relative"
        @click="planSelected = sub.name"
        :class="{ 'plan-selected' : sub.name === planSelected}"
        >
          <div class="left-0 bottom-0" v-if="sub.name === planSelected">
            <Check class="w-8 h-8 fill-current text-white -ml-10"/>
          </div>
          <div class="w-2/5" v-if="billingCycle === 'monthly'">
            <h3 class="hover:text-white">{{sub.name}}</h3>
            <h2 class="text-3xl font-extrabold hover:text-white">${{sub.priceMonth}} <span class="text-lg font-normal">/ month</span></h2>
          </div>
          <div class="w-2/5" v-else>
            <h3 class="hover:text-white">{{sub.name}}</h3>
            <h2 class="text-3xl font-extrabold hover:text-white">${{sub.priceYear}} <span class="text-lg font-normal">/ year</span></h2>
          </div>
          <div class="w-3/5" v-if="billingCycle === 'monthly'">
            <p class="text-sm">{{sub.downloadsMonth}} downloads / month</p>
            <p class="text-sm">{{sub.descriptionOne}}</p>
            <p class="text-sm">{{sub.descriptionTwo}}</p>
          </div>
          <div class="w-3/5" v-else>
            <p class="text-sm">{{sub.downloadsMonth}} downloads / month</p>
            <p class="text-sm">{{sub.descriptionOne}}</p>
            <p class="text-sm">{{sub.descriptionTwo}}</p>
          </div>
        </div>
      </div>
      <div class="w-1/2 flex flex-col justify-center items-start px-4 mt-4">
        <input class="text-align-center w-108 mt-6 h-12 text-center bg-gray-800 rounded-lg text-xl focus:bg-blue-900 outline-none text-white" placeholder="Your Name"/>
        <input class="text-align-center w-108 mt-4 h-12 text-center bg-gray-800 rounded-lg text-xl focus:bg-blue-900 outline-none text-white" placeholder="Your Email"/>
        <input class="text-align-center w-108 mt-4 h-12 text-center bg-gray-800 rounded-lg text-xl focus:bg-blue-900 outline-none text-white" placeholder="Set Your Password"/>
        <input class="text-align-center w-108 mt-4 h-12 text-center bg-gray-800 rounded-lg text-xl focus:bg-blue-900 outline-none text-white" placeholder="Card Number"/>
        <button class="mt-4 bg-yellow-500 p-4 w-108 rounded-lg text-yellow-900 uppercase font-semibold shadow-lg sign-in hover:text-yellow-900">Create My Account</button>
        <h5 class="mt-4 text-white items-center">Includes a 14 day trial before billing begins</h5>
      </div>
    </div>
    <h5 class="mt-24 text-center text-white">Still have questions? <span class="cursor-pointer font-bold hover:underline">You'll find the answers here.</span></h5>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Check from '~/assets/svg/checkmark-outline.svg';

export default {
  components: {
    Logo,
    Check
  },
  data() {
    return {
      billingCycle: 'monthly',
      planSelected: 'Starter',
      subscriptionTypes: [
        {
          name: 'Starter',
          priceMonth: 19,
          priceYear: 190,
          downloadsMonth: 10000,
          descriptionOne: 'Unlimited shows and episodes',
          descriptionTwo: 'Analytics, teams, and more…'
        },
        {
          name: 'Professional',
          priceMonth: 49,
          priceYear: 490,
          downloadsMonth: 50000,
          descriptionOne: 'Unlimited shows and episodes',
          descriptionTwo: 'Analytics, teams, and more…'
        },
        {
          name: 'Small Business',
          priceMonth: 99,
          priceYear: 990,
          downloadsMonth: 150000,
          descriptionOne: 'Unlimited shows and episodes',
          descriptionTwo: 'Analytics, teams, and more…'
        },
      ]
    }
  }
}
</script>

<style>
.sign-in {
  box-shadow: 0px 2px #b67e00;
}

.cycleSelected {
  @apply text-gray-900 px-2 py-1 bg-gray-100 rounded-lg uppercase text-xs font-bold;
}


.plan-selected {
    @apply bg-gray-800 text-white;
}

.selector:not(.cycleSelected):hover {
  @apply text-white;
}
</style>