<template>
    <form class="widget-container relative flex-row">
        <div class="male-female-container flex flex-row">
            <div class="male-container">
                <CGenderSelect :showMaleCalculator="true" :isMaleSelected="this.isMale"
                    @handleClickMale="handleClickMale" />
            </div>
            <div :class="['female-container', { 'move-female-container ': this.isMale }]">
                <CGenderSelect :showMaleCalculator="false" :isMaleSelected="this.isMale"
                    @handleClickFemale="handleClickFemale" />
            </div>
        </div>
        <div v-if="this.isMale" class="calculator-container flex-row bg-white p-3 border-gray-600 border-2 relative">

            <div v-if="(this.placeHolderContent == 'cm')" class="input-fields w-full">
                <CTextInput class="pb-2" labelContent="Altura" placeholderContent="cm" @change="setHeight" />
                <CTextInput class="pb-2" labelContent="Circunferencia de cuello" placeholderContent="cm"
                    @change="setNeck" />
                <CTextInput class="pb-2" labelContent="Circunferencia de cintura" placeholderContent="cm"
                    @change="setWaist" />
            </div>

            <div v-else class="input-fields">
                <div class="flex">
                    <CTextInput class="w-1/2 absolute" labelContent="Altura" placeholderContent="feet"
                        @change="setHeightFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setHeightInches" />
                </div>
                <div class="flex">
                    <CTextInput class="w-1/2 absolute" labelContent="Circunferencia de cuello" placeholderContent="feet"
                        @change="setNeckFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setNeckInches" />
                </div>
                <div class="flex">
                    <CTextInput class=" w-1/2 absolute" labelContent="Circunferencia de cintura"
                        placeholderContent="feet" @change="setWaistFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setWaistInches" />
                </div>
            </div>

            <div class="flex radio-container">
                <CRadio radioTextContent="  Métrico" :isChecked="isMetricSelected" class="m-5 ml-0"
                    @handleRadioChange="handleMetricRadio" />
                <CRadio radioTextContent="  Imperial" :isChecked="isImperialSelected" class="m-5 ml-0"
                    @handleRadioChange="handleImperialRadio" />
            </div>
            <div class="pt-5 text-center button">
                <CButton buttonType="submit" textContent="Calcular" @click="verificateData" />
            </div>
        </div>
        <div v-else-if="!this.isMale"
            class="calculator-container flex-row bg-white p-3 border-gray-600 border-2 relative">

            <div v-if="(this.placeHolderContent == 'cm')" class="input-fields">
                <CTextInput class="pb-2" labelContent="Altura" :placeholderContent="this.placeHolderContent"
                    @change="setHeight" />
                <CTextInput class="pb-2" labelContent="Circunferencia de cuello"
                    :placeholderContent="this.placeHolderContent" @change="setNeck" />
                <CTextInput class="pb-2" labelContent="Circunferencia de cintura"
                    :placeholderContent="this.placeHolderContent" @change="setWaist" />
                <CTextInput class="pb-2" labelContent="Circunferencia de cadera"
                    :placeholderContent="this.placeHolderContent" @change="setHip" />
            </div>

            <div v-else class="input-fields">
                <div class="flex">
                    <CTextInput class="w-1/2 absolute" labelContent="Altura" placeholderContent="feet"
                        @change="setHeightFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setHeightInches" />
                </div>
                <div class="flex">
                    <CTextInput class="w-1/2 absolute" labelContent="Circunferencia de cuello" placeholderContent="feet"
                        @change="setNeckFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setNeckInches" />
                </div>
                <div class="flex">
                    <CTextInput class=" w-1/2 absolute" labelContent="Circunferencia de cintura"
                        placeholderContent="feet" @change="setWaistFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setWaistInches" />
                </div>
                <div class="flex">
                    <CTextInput class=" w-1/2 absolute" labelContent="Circunferencia de cadera"
                        placeholderContent="feet" @change="setHipFeet" />
                    <CTextInput class="mt-8 ml-36 pb-2 w-1/2" labelContent="" placeholderContent="inches"
                        @change="setHipInches" />
                </div>
            </div>

            <div class="flex radio-container">
                <CRadio radioTextContent="  Métrico" :isChecked="isMetricSelected" class="m-5 ml-0"
                    @handleRadioChange="handleMetricRadio" />
                <CRadio radioTextContent="  Imperial" :isChecked="isImperialSelected" class="m-5 ml-0"
                    @handleRadioChange="handleImperialRadio" />
            </div>
            <div class="pt-5 text-center button">
                <CButton buttonType="submit" textContent="Calcular" @click="verificateData" />
            </div>
        </div>
        <div v-if="this.isBfCalculated" class="result-container mt-10 font-normal absolute text-center">
            <CLabel :spanContent="`Su porcentaje de grasa corporal es: ${bfPercentage}`" optionalSymbol="%" />
        </div>
        <div v-else-if="this.isThereError" class="result-container mt-10 font-normal absolute text-center">
            <CLabel :spanContent="`${errorContent}`" />
        </div>
    </form>
</template>

<script>
import CButton from "../components/c-button.vue"
import CTextInput from "../components/c-text-input.vue"
import CLabel from "../components/c-label.vue";
import CRadio from "../components/c-radio.vue";
import CGenderSelect from "../components/c-gender-select.vue"
import { computed } from "vue";

export default {
    name: "w-body-fat-calculator",

    components: {
        CButton,
        CTextInput,
        CLabel,
        CGenderSelect,
        CRadio,
    },

    computed: {
        computedHeigth() {
            this.height = (((this.heightFeet * 12) + this.heightInches) * 2.54);
        },

        computedNeck() {
            this.neckCircumference = (((this.neckFeet * 12) + this.neckInches) * 2.54);
        },

        computedWaist() {
            this.waistCircumference = (((this.waistFeet * 12) + this.waistInches) * 2.54);
        },

        computedHip() {
            this.hipCircumference = (((this.hipFeet * 12) + this.hipInches) * 2.54);
        },

    },

    data() {
        return {
            height: 0,
            neckCircumference: 0,
            waistCircumference: 0,
            hipCircumference: 0,
            bfPercentage: '',
            errorContent: '',
            isBfCalculated: false,
            isThereError: false,
            isMale: true,
            isMetricSelected: false,
            isImperialSelected: true,
            placeHolderContent: "feet",
            heightFeet: 0,
            heightInches: 0,
            neckFeet: 0,
            neckInches: 0,
            waistFeet: 0,
            waistInches: 0,
            hipFeet: 0,
            hipInches: 0,
        };
    },

    methods: {

        //METHOD TO CLEAN DATA FROM THE VARIABLES

        cleanData() {
            this.height = 0;
            this.neckCircumference = 0;
            this.waistCircumference = 0;
            this.hipCircumference = 0;
        },

        //DEFINE METHODS TO GET MESUREMENTS ON FEET/INCHES

        setHeightFeet(e) {
            this.heightFeet = Number(e.target.value);
        },

        setHeightInches(e) {
            this.heightInches = Number(e.target.value)
        },

        setNeckFeet(e) {
            this.neckFeet = Number(e.target.value);
        },

        setNeckInches(e) {
            this.neckInches = Number(e.target.value)
        },

        setWaistFeet(e) {
            this.waistFeet = Number(e.target.value);
        },

        setWaistInches(e) {
            this.waistInches = Number(e.target.value)
        },

        setHipFeet(e) {
            this.hipFeet = Number(e.target.value);
        },

        setHipInches(e) {
            this.hipInches = Number(e.target.value)
        },

        //METHODS TO GET MESUREMENTS ON CM

        setHeight(e) {
            this.height = Number(e.target.value);
        },

        setNeck(e) {
            this.neckCircumference = Number(e.target.value);
        },

        setWaist(e) {
            this.waistCircumference = Number(e.target.value);
        },

        setHip(e) {
            this.hipCircumference = Number(e.target.value);
        },

        //METHODS TO VALIDATE FIELDS

        verificateData() {

            this.computedHeigth;
            this.computedNeck;
            this.computedWaist;
            this.computedHip;

            if (this.isMale) {
                if (((this.height) == 0) || ((this.neckCircumference) == 0) || ((this.waistCircumference) == 0)) {
                    this.isBfCalculated = false;
                    this.isThereError = true;
                    this.errorContent = "Todos los campos deben estar llenos"
                    this.cleanData();
                }
                else {
                    if (isNaN(this.height) || isNaN(this.neckCircumference) || isNaN(this.waistCircumference)) {
                        this.isBfCalculated = false;
                        this.isThereError = true;
                        this.errorContent = "Solo puedes introducir números"
                        this.cleanData();
                    }
                    else {
                        this.calculateBodyFat();
                    }
                }
            }
            else {
                if (((this.height) == 0) || ((this.neckCircumference) == 0) || ((this.waistCircumference) == 0) || ((this.hipCircumference) == 0)) {
                    this.isBfCalculated = false;
                    this.isThereError = true;
                    this.errorContent = "Todos los campos deben estar llenos"
                    this.cleanData();
                }
                else {
                    if (isNaN(this.height) || isNaN(this.neckCircumference) || isNaN(this.waistCircumference) || isNaN(this.hipCircumference)) {
                        this.isBfCalculated = false;
                        this.isThereError = true;
                        this.errorContent = "Solo puedes introducir números"
                        this.cleanData();
                    }
                    else {
                        this.calculateBodyFat();
                    }
                }
            }
        },

        //METHOD TO CALCULATE BF AND HANDLE THE OUTPUT

        calculateBodyFat() {

            if (this.isMale) {
                this.bfPercentage = (495 / (1.0324 - 0.19077 * (Math.log10(this.waistCircumference - this.neckCircumference)) + 0.15456 * (Math.log10(this.height))) - 450).toFixed(2);
            }
            else {
                this.bfPercentage = (495 / (1.29579 - 0.35004 * (Math.log10(this.waistCircumference + this.hipCircumference - this.neckCircumference)) + 0.22100 * (Math.log10(this.height))) - 450).toFixed(2);
            }

            if ((this.bfPercentage <= 0) || (isNaN(this.bfPercentage)) || (this.bfPercentage >= 100)) {
                this.isBfCalculated = false;
                this.isThereError = true;
                this.errorContent = "Error de calculo. Asegurese de que los datos introducidos son correctos."
                this.cleanData();
            }
            else {
                this.isBfCalculated = true
            }
        },

        //METHODS TO HANDLE EVENTS

        handleClickMale() {
            this.isMale = true;
            this.isBfCalculated = false;
        },

        handleClickFemale() {
            this.isMale = false;
            this.isBfCalculated = false;
        },

        handleMetricRadio(e) {
            this.isMetricSelected = true;
            this.isImperialSelected = false;
            this.placeHolderContent = "cm"
        },

        handleImperialRadio(e) {
            this.isMetricSelected = false;
            this.isImperialSelected = true;
            this.placeHolderContent = "feet"
        },
    },
}
</script>

<style>
.calculator-container {
    border-radius: 2%;
    border-top-left-radius: 0%;
    z-index: 1;
    width: 300px;
}

.move-female-container {
    margin-left: 32%;
}
</style>
