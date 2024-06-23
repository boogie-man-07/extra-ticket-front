<template>
    <main>
        <TicketListComponent  @change-tg-button-state="changeTgButtonState" @set-selected-item-id="setSelectedItemId" />
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
        chatData: {},
        selectedItemId: 0
      }
    },
    mounted() {
        const tg = window.Telegram.WebApp
        this.chatData = tg.initDataUnsafe

        tg.MainButton.setParams({
            text: 'Выбрать событие',
            color: '#0D488C'
        })
        tg.MainButton.onClick(this.send)

        tg.expand()
    },
    methods: {
        changeTgButtonState(state) {
        const tg = window.Telegram.WebApp
        if (state) {
            tg.MainButton.show()
        } else {
            tg.MainButton.hide()
        }
        },
        setSelectedItemId(id) {
            this.selectedItemId = id
        },
    },
  }
  
  </script>