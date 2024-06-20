<template>
    <div class="info-paragraph text-center">
        <span class="paragraph-title font-bold underline">{{ paragraphTitle }}</span>
        <p class="paragraph-content text-justify"><br>{{ paragraphContent }}</p>
    </div>
</template>

<script>
export default {
    name: "c-info-paragraph",

    props: {
        paragraphTitle: { type: String },
        paragraphContent: { type: String },
    }
}
</script>

<style></style>