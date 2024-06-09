<script>
import CButton from "../components/c-button.vue"
import CTextInput from "../components/c-text-input.vue"
import CLabel from "../components/c-label.vue";

export default {
    name: "w-body-fat-calculator",

    components: {
        CButton,
        CTextInput,
        CLabel,
    },

    data() {
        return {
            height: '',
            neckCircumference: '',
            waistCircumference: '',
            bfPercentage: '',
            isBfCalculated: false,
        };
    },

    methods: {
        calculateBodyFat(e) {
            e.preventDefault;

            // console.log("Altura: " + this.height)
            // console.log("Cuello: " + this.neckCircumference)
            // console.log("Cintura: " + this.waistCircumference)

            this.bfPercentage = (495 / (1.0324 - 0.19077 * (Math.log10(this.waistCircumference - this.neckCircumference)) + 0.15456 * (Math.log10(this.height))) - 450).toFixed(2);

            this.isBfCalculated = true
            // console.log(this.bfPercentage);
        }
    }
}
</script>

<template>
    <form class="widget-container relative">
        <div class="calculator-container flex-row bg-white p-3 border-gray-600 border-2">
            <div>
                <CTextInput autocomplete="on" class="pb-2" labelContent="Altura" placeholderContent="cm"
                    @change="(e) => { this.height = parseInt(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cuello"
                    placeholderContent="cm" @change="(e) => { this.neckCircumference = parseInt(e.target.value) }" />
                <CTextInput autocomplete="on" class="pb-2" labelContent="Circunferencia de cintura"
                    placeholderContent="cm" @change="(e) => { this.waistCircumference = parseInt(e.target.value) }" />
            </div>
            <div class="pt-5 text-center">
                <CButton textContent="Calcular" @click="calculateBodyFat" />
            </div>
        </div>
        <div v-if="this.isBfCalculated" class="result-container mt-10 font-normal underline absolute text-center">
            <CLabel :bfPercentage="this.bfPercentage" />
        </div>
    </form>
</template>

<style>
.calculator-container {
    border-radius: 2%;
}
</style>