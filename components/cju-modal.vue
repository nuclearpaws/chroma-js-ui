<template>
    <div class="modal" v-if="show">
        <div class="modal-overlay" v-on:click="closeModal"></div>
        <div class="modal-content">
            <slot />
            <button v-on:click="closeModal">Close</button>
        </div>
    </div>
</template>

<script lang="ts" setup>
interface Props {
    show: Boolean;
}

const props = defineProps<Props>();
const emit = defineEmits(["update:show"]);

function closeModal() {
    emit("update:show", false);
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
    z-index: 1000;
}

.modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: -1; /* Place the overlay behind the modal content */
}

.modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
    z-index: 1; /* Place the modal content in front of the overlay */
}
</style>
