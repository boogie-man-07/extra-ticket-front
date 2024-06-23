<template>
    <el-row class="search-card">
        <el-col>
            <el-input
                class="custom-input"
                @focus="focused = true"
                @blur="focused = false"
                v-model="filteredValue"
                type="text"
                placeholder="Поиск события"
                @clear="clearInput"
                clearable
            />
        </el-col>
    </el-row>
    <template v-if="ticketsList.length > 0">
        <el-row :class="focused ? 'employee-box-with-padding' : 'employee-box'">
            <template  v-for="ticket in ticketsList" :key="ticket.id">
                <TicketsListItemComponent :ticket="ticket" @select-item="selectItem" />
            </template>
        </el-row>
    </template>
</template>

<script>
import TicketsListItemComponent from "@/components/TicketsListItemComponent.vue"

export default {
    "name": "TicketListComponent",
    components: {
        TicketsListItemComponent
    },
    emits: ['change-tg-button-state', 'set-selected-item-id'],
    data() {
        return {
            filteredValue: '',
            focused: false,
            tickets: [
                { id: 1, title: 'Самые известные комики', place: "Стендап бар \"Патрики\"", date: "22:00 28.06.2024", "price": "от 1650 р", "image": "https://media.ticketland.ru/images/420x270/81/7d/817d69d77f92f77fad5cbdc69e96fcce.jpg", isSelected: false },
                { id: 2, title: 'Unki', place: "Клуб \"Урбан\"", date: "18:00 30.06.2024", "price": "999 - 2900 р", "image": "https://media.ticketland.ru/images/420x270/ed/e1/ede1b538bd7e4a601ff4afc78ea6e7fa.jpg", isSelected: false },
                { id: 3, title: 'Ничего не бойся, я с тобой', place: "МДМ", date: "19:00 25.06.2024", "price": "1300 - 10000 р", "image": "https://media.ticketland.ru/images/420x270/f9/ad/f9ad2ef01e423be6a607da2af01d7b37.jpg", isSelected: false }
            ],
        }
    },
    watch: {
        isAnySelected() {
            if (this.isAnySelected) {
                this.$emit('change-tg-button-state', true)
            } else {
                this.$emit('change-tg-button-state', false)
            }
        },
    },
    methods: {
        selectItem(id) {
            this.tickets.forEach(el => {
                el.id == id ? el.isSelected = !el.isSelected : el.isSelected = false
            });
            const currentItem = this.tickets.filter(el => el.isSelected)
            this.$emit('set-selected-item-id', currentItem.length > 0 ? currentItem[0].id : 0)
        },
        clearInput() {
            this.tickets.forEach(el => {
                el.isSelected = false
            });
        },
    },
    computed: {
        ticketsList() {
            return this.tickets.filter(el =>
                !this.filteredValue ||
                el.title.toLowerCase().includes(this.filteredValue.toLowerCase()) ||
                el.place.toLowerCase().includes(this.filteredValue.toLowerCase())
            )
        },
        isAnySelected() {
            return this.tickets.filter(el => el.isSelected == true).length > 0
        },
    },
}
</script>