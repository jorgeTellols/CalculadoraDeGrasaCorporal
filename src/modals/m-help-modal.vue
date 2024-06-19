<template>
    <div class="modal absolute" v-if="visible">
        <div class="modal-overlay" @click="close"></div>
        <div class="modal-content">
            <p>This is the content inside the modal.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "m-help-modal",

    props: {
        visible: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        close() {
            this.$emit('close');
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
</style>