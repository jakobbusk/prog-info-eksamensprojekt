<template>
      <!-- Page header -->
      <div class="bg-white shadow mb-8 " >
        <div class="px-4 sm:px-6 lg:max-w-6xl lg:mx-auto lg:px-8">
          <div class="py-6 md:flex md:items-center md:justify-between lg:border-t lg:border-gray-200">
            <div class="flex-1 min-w-0">
              <!-- Profile -->
              <div class="flex items-center">
                <img src="@/assets/images/profilbillede.png" class="hidden h-16 rounded-full sm:block" alt="">
                <div>
                  <div class="flex items-center">
                    <img class="h-16 w-16 rounded-full sm:hidden" src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixqx=OX1g42jy4V&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2.6&w=256&h=256&q=80" alt="">
                    <h1 class="ml-3 text-2xl font-bold leading-7 text-gray-900 sm:leading-9 sm:truncate">
                      {{grettingMessage}}, Jakob Busk
                    </h1>
                  </div>
                  <dl class="mt-6 flex flex-col sm:ml-3 sm:mt-1 sm:flex-row sm:flex-wrap">
                    <dt class="sr-only">Company</dt>
                    <dd class="flex items-center text-sm text-gray-500 font-medium capitalize sm:mr-6">
                      <!-- Heroicon name: solid/office-building -->
                      <svg class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                        <path fill-rule="evenodd" d="M4 4a2 2 0 012-2h8a2 2 0 012 2v12a1 1 0 110 2h-3a1 1 0 01-1-1v-2a1 1 0 00-1-1H9a1 1 0 00-1 1v2a1 1 0 01-1 1H4a1 1 0 110-2V4zm3 1h2v2H7V5zm2 4H7v2h2V9zm2-4h2v2h-2V5zm2 4h-2v2h2V9z" clip-rule="evenodd" />
                      </svg>
                      Busken A/S
                    </dd>
                  </dl>
                </div>
              </div>
            </div>
            <div class="mt-6 flex space-x-3 md:mt-0 md:ml-4">
              <router-link :to="{name: 'expense-new'}" class="inline-flex items-center px-4 py-2 border border-gray-300 shadow-sm text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-cyan-500">
                Bogfør udgift
              </router-link>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
// @ is an alias to /src
// import axios from 'axios';


export default {
  name: 'PageHeader',
  components: {
    
  },
  data() {
    return {
      grettingMessage: null,

    } 
  },

  created() {
    this.greeting();
  },
  beforeRouteUpdate() {
    this.greeting();

  },

  methods: {
    greeting () {
      var thehours = new Date().getHours();
      var nat = 'God nat'
      var morgen = 'God morgen'
      var formiddag = 'God formiddag'
      var eftermiddag = 'God eftermiddag'
      var aften = 'God aften'

      if (thehours < 6) {
        this.grettingMessage = nat;
        console.log(this.grettingMessage)
      } else if (thehours >= 6 && thehours < 9) {
        this.grettingMessage = morgen; 
        console.log(this.grettingMessage)
      } else if (thehours >= 9 && thehours < 12) {
        this.grettingMessage = formiddag; 
        console.log(this.grettingMessage)
      } else if (thehours >= 12 && thehours < 18) {
        this.grettingMessage = eftermiddag;
        console.log(this.grettingMessage) 
      } else if (thehours >= 18 && thehours < 23) {
        this.grettingMessage = aften; 
        console.log(this.grettingMessage)
      }else {
        this.grettingMessage = nat;
        console.log(this.grettingMessage)
      }
      console.log(this.grettingMessage)
    }
  }
}
</script>