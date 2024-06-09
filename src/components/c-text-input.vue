<script>
export default {
    name: "c-text-input",

    props: {
        labelContent: { type: String },
        placeholderContent: { type: String },
    },
};
</script>

<template>
    <div class="flex-row">
        <div class="label">
            <label>{{ labelContent }}</label>
        </div>
        <div class="input-box mt-2 border-2 border-black">
            <input class="placeholder-right" :placeholder=placeholderContent type="text" />
        </div>
    </div>
</template>

<style>
.placeholder-right::placeholder {
    text-align: right;
    margin-right: 5px;
}

/* Ensure the user input is aligned left */
.placeholder-right {
    text-align: left;
}
</style>
