<template>
    <div>
        <div v-if="labelContent !== ''" class="label">
            <label class="whitespace-nowrap">{{ labelContent }}</label>
        </div>
        <div class="input-box mt-2 border-2 border-black">
            <input class="w-full placeholder-right" :placeholder=placeholderContent type="text" />
        </div>
    </div>
</template>

<script>
export default {
    name: "c-text-input",

    props: {
        labelContent: { type: String },
        placeholderContent: { type: String },
    },
};
</script>

<style>
input::placeholder {
    text-align: right;
    margin-right: 5px;
}

input {
    text-align: right
}

input:focus {

    outline: 0;
}
</style>
