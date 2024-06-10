<template>
    <button :type="this.buttonType" @click="(e) => e.preventDefault()">{{ textContent }}</button>
</template>

<script>
export default {
    name: "c-button",

    props: {
        textContent: { type: String },
        buttonType: { type: String },
    },
};
</script>

<style>
button {
    background-color: #6699cc;
    padding: 5px 40px;
    border-radius: 25%;
}
</style>
