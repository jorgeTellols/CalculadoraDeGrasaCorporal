<template>
    <span>{{ spanContent }}{{ optionalSymbol }}</span>
</template>

<script>
export default {
    name: "c-label",

    props: {
        spanContent: { type: String },
        optionalSymbol: { type: String },
    },
}
</script>

<style></style>