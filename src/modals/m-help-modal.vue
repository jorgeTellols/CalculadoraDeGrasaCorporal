<template>
    <transition class="modal-animation">
        <div class="modal absolute" v-if="visible">
            <div class="modal-overlay" @click="closeModal"></div>
            <div class="modal-content">
                <CInfoParagraph paragraphTitle="¿Qué es todo esto?" paragraphContent="Lo que tienes delante es una calculadora para medir tu porcentaje de grasa corporal, es decir, 
                la cantidad porcentual de grasa respecto a tu masa osea y tu masa magra. Es bastante util a la hora de realizar un 
                seguimiento de pérdida de grasa." />
                <br>
                <CInfoParagraph paragraphTitle="¿En base a qué se calcula?" paragraphContent="Existen diferentes formas de calcular la grasa corporal, ya sea mediante escaneres fisicos 
                o formulas matematicas. La formula que se tiene en consideración aquí fue diseñada por el cuerpo de marines 
                del ejercito de Estados Unidos y calcula el resultado en base a una serie de medidas corporales." />
                <br>
                <CInfoParagraph paragraphTitle="¿Como me tomo las médidas corporales?" paragraphContent="Usa una cinta de medir para calcular la circunferencia en los mismo lugares de tu cuerpo que los 
            marcados por la linea negra en las siguientes imagenes" />
                <br>
                <div class="flex justify-evenly">
                    <img class="w-56 h-full" src="../assets/man.jpg">
                    <img class="w-48 h-full" src="../assets/woman.jpg">
                </div>
                <br>
                <CInfoParagraph paragraphTitle="Videotutorial del proceso" />
                <div class="flex justify-center">
                    <iframe width="530" height="423" src="https://www.youtube.com/embed/AYYiqi2hWk0"
                        title="USMC Body Composition Program – Self-Tensioning Taping Device Usage"
                        allowfullscreen></iframe>
                </div>
                <br>
                <CInfoParagraph paragraphTitle="Formula para el cálculo de grasa corporal en hombres" />
                <img class="text-center" src="../assets/calculo_hombres.jpg" />
                <br>
                <CInfoParagraph paragraphTitle="Formula para el cálculo de grasa corporal en mujeres" />
                <img class="text-center" src="../assets/calculo_mujeres.jpg" />
            </div>
        </div>
    </transition>
</template>

<script>
import CInfoParagraph from "../components/c-info-paragraph.vue";

export default {
    name: "m-help-modal",

    components: {
        CInfoParagraph
    },

    props: {
        visible: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        closeModal() {
            this.$emit('closeModal');
        }
    }
}
</script>

<style scoped>
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0, 0, 0, 0.5);
}

.modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.modal-content {
    position: relative;
    background: white;
    padding: 20px;
    border-radius: 5px;
    z-index: 3;
    width: 50%;
    height: 50%;
    overflow: scroll;
    transition: cubic-bezier(0.6, 0.04, 0.98, 0.335)
}

.modal-close {
    position: absolute;
    top: 10px;
    right: 10px;
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
}

.modal-animation-enter-active {
    transition: all 9s ease;
}
</style>