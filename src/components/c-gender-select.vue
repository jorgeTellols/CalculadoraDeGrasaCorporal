<template>
    <h1 class="male-select" @click="handleClickMale">Hombre</h1>
    <h1 class="female-select" @click="handleClickFemale">Mujer</h1>
</template>

<script>
export default {
    name: "c-gender-select",

    emits: ['handleClickMale', 'handleClickFemale'],

    data() {
        return {
            localMaleSelected: this.isMaleSelected,
            localFemaleSelected: !this.localMaleSelected,
        };
    },

    // props: {
    //     isMaleSelected,
    // },

    methods: {
        handleClickMale() {
            this.$emit('handleClickMale');
        },
        handleClickFemale() {
            this.$emit('handleClickFemale');
        }
    }
}

</script>


<style>
.male-select,
.female-select {
    border-color: #4a5568;
    border-width: 2px 2px 0 2px;
    border-style: solid;
    background-color: white;
    padding: 2%;
    border-radius: 5%;
    user-select: none;
}

.female-select {
    border-width: 2px 2px 0 0;
}

.male-select:hover,
.female-select:hover {
    cursor: pointer;
}

.male-select::isMaleSelected {
    cursor: pointer;
    padding-bottom: 2.8%;
    z-index: 2;
    position: absolute;
    border-bottom-left-radius: 0%;
    border-bottom-right-radius: 0%;
}
</style>