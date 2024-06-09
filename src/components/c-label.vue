<script>
export default {
    name: "c-label",

    props: {
        bfPercentage: { type: String },
    },
}
</script>

<template>
    <span>Tu porcentaje de grasa corporal es: {{ bfPercentage }}%</span>
</template>

<style></style>