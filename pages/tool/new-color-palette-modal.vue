<template>
    <cju-modal v-model:show="show">
        <h1>Edit Color Palette</h1>
        <hr />
        <cju-color-picker
            name="Start Color"
            id="start-color"
            v-model:value="start"
        />
        <cju-color-picker name="Mid Color" id="mid-color" v-model:value="mid" />
        <cju-color-picker name="End Color" id="end-color" v-model:value="end" />
        <hr />
        <button v-on:click="addColorPalette()">Add</button>
    </cju-modal>
</template>

<script lang="ts" setup>
interface Props {
    show: boolean;
}

const props = defineProps<Props>();
const emit = defineEmits(["update:show", "addPalette"]);

const start = ref<string>("#ff0000");
const mid = ref<string>("#00ff00");
const end = ref<string>("#0000ff");

const show = computed({
    get: () => props.show,
    set: (value) => emit("update:show", value),
});

function addColorPalette() {
    emit("addPalette", {
        mid: mid.value,
        start: start.value,
        end: end.value,
    });
    show.value = false;
}
</script>

<style scoped></style>
