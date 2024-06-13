<template>
    <div class="radio-button">
        <input type="radio" :checked="this.isChecked" @click="handleRadioChange">{{ radioTextContent
        }}</input>
    </div>
</template>

<script>
export default {
    name: "c-radio",

    methods: {
        handleRadioChange(e) {
            this.$emit('handleRadioChange', e);
        }
    },

    props: {
        radioTextContent: { type: String },
        isChecked: { type: Boolean },
    },
}
</script>

<style></style>