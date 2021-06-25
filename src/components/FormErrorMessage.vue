<template>
    <span class="text-danger">{{ errors[0] }}</span>
</template>

<script>
export default {
    props:{
        errors:{
            type:Array,
            required: true
        }
    }
}
</script>

<style scoped>

</style>