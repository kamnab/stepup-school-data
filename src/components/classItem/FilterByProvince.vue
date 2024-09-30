<script setup>

const props = defineProps({
    provinceList: {
        name: String,
        count: Number
    }
})


</script>

<template>
    <div class="text-muted mt-3"></div>
    <div class="d-flex flex-wrap border">
        <div class="p-2" v-for="(province, index) in provinceList" :key="index">{{ province.name }}: <span
                class="text- me-1">{{
                    province.count }}</span></div>
    </div>

</template>