<template>
    <main>
        <TicketListComponent />
    </main>
</template>
  
  <script>
  import TicketListComponent from '@/components/TicketListComponent.vue'
  
  export default {
    name: "TicketsListView",
    components: {
        TicketListComponent
    },
    data() {
      return {
      }
    },
    mounted() {
    },
    methods: {
    },
  }
  
  </script>