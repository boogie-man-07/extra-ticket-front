<template>
    <el-row>
        <el-col>
            <el-card class="search-card" :class="ticket.isSelected ? 'selected-card' : 'deselected-card'" shadow="hover" @click="chooseEvent(ticket)" style="max-width: 480px">
                <template #header>
                    <el-row>
                        <el-col>
                            <el-text class="ticket-title">{{ ticket.title }}</el-text>
                        </el-col>
                        <el-col>
                            <el-text class="ticket-place">{{ ticket.place }}</el-text>
                        </el-col>
                    </el-row>
                </template>
                <el-row>
                    <el-col :span="12">
                        <el-text class="ticket-date">{{ ticket.date }}</el-text>
                    </el-col>
                    <el-col :span="12">
                        <el-text class="ticket-price">{{ ticket.price }}</el-text>
                    </el-col>
                </el-row>
                <el-row style="margin: 8px 0px;">
                    <el-col>
                        <img
                            :src="ticket.image"
                            style="width: 100%;"
                        />
                    </el-col>
                </el-row>
            </el-card>
        </el-col>
    </el-row>
</template>

<script>

export default {
    "name": "TicketsListItemComponent",
    emits: ['select-item'],
    props: {
        ticket: Object
    },
    methods: {
        chooseEvent(item) {
            this.$emit('select-item', item.id)
            console.log(item)
        }
    },
}
</script>