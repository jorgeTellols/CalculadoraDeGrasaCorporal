<template>
    <div v-if="showMaleCalculator" :class="['male-select', { 'selected-male': isMaleSelected, }]"
        @click="handleClickMale">
        <h1 class="p-1">Hombre </h1>
    </div>
    <div v-else :class="['female-select', { 'selected-female': !isMaleSelected }]" @click="handleClickFemale">
        <h1 class="p-1">Mujer </h1>
    </div>
</template>

<script>
export default {
    name: "c-gender-select",

    emits: ['handleClickMale', 'handleClickFemale'],

    data() {
        return {
            localMaleSelected: this.isMaleSelected,
        };
    },

    props: {
        isMaleSelected: { type: Boolean },
        showMaleCalculator: { type: Boolean },
    },

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
    padding: 0%;
    border-radius: 5%;
    user-select: none;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
}

.female-select {
    border-width: 2px 2px 0 0;
}

.male-select:hover,
.female-select:hover {
    cursor: pointer;
}

.selected-male {
    z-index: 2;
    padding-bottom: 0.8%;
    cursor: default;
    position: absolute;
    border-bottom-left-radius: 0%;
    border-bottom-right-radius: 0%;
}

.selected-female {
    z-index: 2;
    padding-bottom: 0.8%;
    position: absolute;
    border-bottom-left-radius: 0%;
    border-bottom-right-radius: 0%;
}

.selected-male:hover,
.selected-female:hover {
    cursor: default;
}
</style>