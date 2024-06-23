<template>
    <el-row class="search-card">
        <el-col>
            <el-card style="max-width: 480px">
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
    props: {
        ticket: Object
    },
}
</script>