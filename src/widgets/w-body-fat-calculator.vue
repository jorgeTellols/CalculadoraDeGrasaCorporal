<template>
    <form class="widget-container relative" autocomplete="on">
        <div class="male-female-container flex">
            <CGenderSelect @handleClickMale="this.isMale = true" @handleClickFemale="this.isMale = false" />
        </div>
        <div v-if="this.isMale" class=" calculator-container flex-row bg-white p-3 border-gray-600 border-2 relative">
            <div class="input-fields">
                <CTextInput autocomplete="on" class="pb-2" labelContent="Altura" placeholderContent="cm"
                    @change="(e) => { this.height = Number(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cuello"
                    placeholderContent="cm" @change="(e) => { this.neckCircumference = Number(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cintura"
                    placeholderContent="cm" @change="(e) => { this.waistCircumference = Number(e.target.value) }" />
            </div>
            <div class="pt-5 text-center button">
                <CButton buttonType="submit" textContent="Calcular" @click="verificateData" />
            </div>
        </div>
        <div v-else-if="this.isFemale"
            class=" calculator-container flex-row bg-white p-3 border-gray-600 border-2 relative">
            <div class="input-fields">
                <CTextInput autocomplete="on" class="pb-2" labelContent="Altura" placeholderContent="cm"
                    @change="(e) => { this.height = Number(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cuello"
                    placeholderContent="cm" @change="(e) => { this.neckCircumference = Number(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cintura"
                    placeholderContent="cm" @change="(e) => { this.waistCircumference = Number(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cadera"
                    placeholderContent="cm" @change="(e) => { this.hipCircumference = Number(e.target.value) }" />
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
import CGenderSelect from "../components/c-gender-select.vue"

export default {
    name: "w-body-fat-calculator",

    components: {
        CButton,
        CTextInput,
        CLabel,
        CGenderSelect,
    },

    data() {
        return {
            height: '',
            neckCircumference: '',
            waistCircumference: '',
            hipCircumference: '',
            bfPercentage: '',
            errorContent: '',
            isBfCalculated: false,
            isThereError: false,
            isMale: true,
            isFemale: !this.isMale,
        };
    },

    methods: {
        verificateData() {
            if (((this.height) == '') || ((this.neckCircumference) == '') || ((this.waistCircumference) == '')) {
                this.isBfCalculated = false;
                this.isThereError = true;
                this.errorContent = "Todos los campos deben estar llenos"
            }
            else {
                if (isNaN(this.height) || isNaN(this.neckCircumference) || isNaN(this.waistCircumference)) {
                    this.isBfCalculated = false;
                    this.isThereError = true;
                    this.errorContent = "Solo puedes introducir números"
                }
                else {
                    this.calculateBodyFat();

                    if ((this.bfPercentage <= 0) || (isNaN(this.bfPercentage)) || (this.bfPercentage >= 100)) {
                        this.isBfCalculated = false;
                        this.isThereError = true;
                        this.errorContent = "Error de calculo. Asegurese de que los datos introducidos son correctos."
                    }
                    else {
                        this.isBfCalculated = true
                    }
                }
            }
        },

        calculateBodyFat() {

            if (this.isMale) {
                this.bfPercentage = (495 / (1.0324 - 0.19077 * (Math.log10(this.waistCircumference - this.neckCircumference)) + 0.15456 * (Math.log10(this.height))) - 450).toFixed(2);
            }
            else {
                this.bfPercentage = (495 / (1.0324 - 0.19077 * (Math.log10(this.waistCircumference + this.hipCircumference - this.neckCircumference)) + 0.15456 * (Math.log10(this.height))) - 450).toFixed(2);
            }
        },

        clickMale() {
            console.log("Has clickado hombre")
        },

        clickFemale() {
            console.log("Has clickado mujer")
        }
    },
}
</script>

<style>
.calculator-container {
    border-radius: 2%;
    border-top-left-radius: 0%;
    z-index: 1;
}
</style>