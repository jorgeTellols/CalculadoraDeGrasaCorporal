<script>
export default {
    name: "c-button",

    props: {
        textContent: { type: String },
    },
};
</script>

<template>
    <button type="button">{{ textContent }}</button>
</template>

<style>
button {
    background-color: #6699cc;
    padding: 5px 40px;
    border-radius: 25%;
}
</style>
