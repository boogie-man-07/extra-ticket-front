<template>
    <el-row class="search-card">
        <el-col>
            <el-date-picker
                v-model="selectedDate"
                type="date"
                placeholder="Выберите дату"
                format="DD.MM.YYYY"
                value-format="YYYY-MM-DD"
                style="width: 100%; height: 50px; margin: 4px 0px;"
            />
        </el-col>
        <el-col>
            <el-select
                class="custom-select"
                v-model="selectedPlace"
                placeholder="Выберите место"
            >
                <template v-for="place in places" :key="place.id">
                    <el-option :label="place.value" :value="place.value" />
                </template>
            </el-select>
        </el-col>
        <el-col>
            <el-select
                class="custom-select"
                v-model="selectedCategory"
                placeholder="Выберите категорию"
            >
                <template v-for="category in categories" :key="category.id">
                    <el-option :label="category.value" :value="category.value" />
                </template>
            </el-select>
        </el-col>
    </el-row>
</template>

<script>
import EmployeeItemComponent from "@/components/EmployeeItemComponent.vue"

export default {
    "name": "HomeComponent",
    components: {
        EmployeeItemComponent
    },
    emits: ['change-tg-button-state', 'set-selected-item-id'],
    data() {
        return {
            selectedDate: null,
            selectedPlace: null,
            selectedCategory: null,
            places: [
                { id: 1, value: 'Москва' },
                { id: 2, value: 'Санкт-Петербург' }
            ],
            categories: [
                { id: 1, value: 'Спектакли' },
                { id: 2, value: 'Концерты' },
                { id: 3, value: 'Фестивали' },
                { id: 4, value: 'Мюзиклы' },
                { id: 5, value: 'Детям' },
                { id: 6, value: 'Классика' },
                { id: 7, value: 'Стендап' }
            ],
        }
    },
    methods: {
        selectItem(id) {
            this.employees.forEach(el => {
                el.id == id ? el.isSelected = !el.isSelected : el.isSelected = false
            });
            const currentItem = this.employees.filter(el => el.isSelected)
            this.$emit('set-selected-item-id', currentItem.length > 0 ? currentItem[0].id : 0)
        },
        clearInput() {
            this.employees.forEach(el => {
                el.isSelected = false
            });
        },
    },
    computed: {
    },
}
</script>