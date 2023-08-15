<template>
    <cju-modal v-model:show="showColorPaletteModal">
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
        <button v-on:click="saveColorPalette()">Save</button>
    </cju-modal>
    <cju-color-palette v-bind:colors="colors" />
    <button v-on:click="showColorPaletteModal = true">Edit</button>
    <button v-on:click="deleteColorPalette()">Delete</button>
    <hr />
</template>

<script lang="ts" setup>
import chroma from "chroma-js";

interface Props {
    start: string;
    mid: string;
    end: string;
}

const props = defineProps<Props>();
const emit = defineEmits([
    "update:start",
    "update:main",
    "update:end",
    "deleteColorPalette",
]);

const classes = [0.05, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 0.95];

const showColorPaletteModal = ref<boolean>(false);

const start = computed({
    get: () => props.start,
    set: (value) => emit("update:start", value),
});

const mid = computed({
    get: () => props.mid,
    set: (value) => emit("update:main", value),
});

const end = computed({
    get: () => props.end,
    set: (value) => emit("update:end", value),
});

const colors = computed(() =>
    chroma
        .scale([props.start, props.mid, props.end])
        .classes(classes)
        .colors(classes.length)
);

function saveColorPalette() {
    showColorPaletteModal.value = false;
}

function deleteColorPalette() {
    emit("deleteColorPalette");
}
</script>

<style scoped></style>
