<template>
<main class="bg-gray-100 flex-1 relative pb-8 z-0 overflow-y-auto ">
    <page-header />
    <div v-if="expense" class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
        <!-- This example requires Tailwind CSS v2.0+ -->
        <div class="bg-white text-left shadow overflow-hidden sm:rounded-lg ">
        <div class="px-4 py-5 sm:px-6">
            <h3 class="text-lg leading-6 font-medium text-gray-900">
            Udgift Information
            </h3>
            <p class="mt-1 max-w-2xl text-sm text-gray-500">
            Oprettet af {{expense.created_by}}
            </p>
        </div>
        <div class="border-t border-gray-200">
            <dl>
            <div class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Navn
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.expense_name }}
                </dd>
            </div>
            <div class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Note
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.expense_notes }}
                </dd>
            </div>
            <div class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Udgiftskategori
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.expense_category }}
                </dd>
            </div>
            <div class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Udgiftsdato
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.due_date}}
                </dd>
            </div>
            <div class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Udgiftsbeløb
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.amount }} DKK
                </dd>
            </div>
            <div class="bg-white px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Moms
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                {{ expense.tax }} DKK
                </dd>
            </div>
            <div class="bg-gray-50 px-4 py-5 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
                <dt class="text-sm font-medium text-gray-500">
                Udgiftsbilag
                </dt>
                <dd class="mt-1 text-sm text-gray-900 sm:mt-0 sm:col-span-2">
                <ul class="border border-gray-200 rounded-md divide-y divide-gray-200">
                    <li v-for="(attachment, idx) in expense.attachments" :key="attachment"  class="pl-3 pr-4 py-3 flex items-center justify-between text-sm">
                    <div class="w-0 flex-1 flex items-center">
                        <!-- Heroicon name: solid/paper-clip -->
                        <svg class="flex-shrink-0 h-5 w-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                        <path fill-rule="evenodd" d="M8 4a3 3 0 00-3 3v4a5 5 0 0010 0V7a1 1 0 112 0v4a7 7 0 11-14 0V7a5 5 0 0110 0v4a3 3 0 11-6 0V7a1 1 0 012 0v4a1 1 0 102 0V7a3 3 0 00-3-3z" clip-rule="evenodd" />
                        </svg>
                        <span class="ml-2 flex-1 w-0 truncate">
                        {{ attachment.name }}
                        </span>
                    </div>
                    <div class="ml-4 flex-shrink-0">
                        <a :href="idx" class="font-medium text-indigo-600 hover:text-indigo-500">
                        Download
                        </a>
                    </div>
                    </li>
                </ul>
                </dd>
            </div>
            </dl>
        </div>
        </div>
    </div>
</main>

</template>

<script>
import PageHeader from '@/components/PageHeader'
export default {
  components: {
    PageHeader
  },
  data () {
    return {
      expense: null,
      errors: [],
    }
  },
  created() {
    // kalder funktionen getExpense når komponenter bliver lavet
    this.getExpense(this.$route.params.id);
  },
  beforeRouteUpdate(to, from, next) {
    // kalder funktionen getExpense når komponenter bliver genindlæst
    this.getExpense(to.params.id, from, next)
  },
  methods: {
    // Fetches udgiften efter komponentet er indlæst eller genindlæst
    async getExpense(id, from, next) {
        try {
          const response = await this.$axios.get("/expense/" + id )
          this.expense = response.data
          console.log(response.data);
          next()
        } catch (err) {
          this.errors.push(err)
        }
      },
      fetchData(response) {
      this.expense = response.data;
    },
  }
}
</script>