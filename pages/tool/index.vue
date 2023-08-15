<template>
    <new-color-palette-modal
        v-model:show="showAddColorPaletteModal"
        v-on:add-palette="(newPallete) => addPallete(newPallete)"
    />
    <h1>Tool</h1>
    <hr />
    <div v-if="colorPalettes.length > 0">
        <h2>Palettes:</h2>
        <br />
        <color-palette
            v-for="colorPalette in colorPalettes"
            v-bind:key="
                colorPalette.start + colorPalette.mid + colorPalette.end
            "
            v-model:start="colorPalette.start"
            v-model:mid="colorPalette.mid"
            v-model:end="colorPalette.end"
            v-on:delete-color-palette="deleteColorPalette(colorPalette)"
        />
    </div>
    <button v-on:click="showAddColorPaletteModal = true">
        Add Color Palette
    </button>
    <button
        v-on:click="clearColorPalettes()"
        v-bind:disabled="colorPalettes.length <= 0"
    >
        Clear Color Palettes
    </button>
    <hr />
</template>

<script lang="ts" setup>
import ColorPalette from "./color-palette.vue";
import NewColorPaletteModal from "./new-color-palette-modal.vue";

const showAddColorPaletteModal = ref<boolean>(false);

const colorPalettes = ref<{ mid: string; start: string; end: string }[]>([]);

function deleteColorPalette(colorPalette: {
    mid: string;
    start: string;
    end: string;
}) {
    const index = colorPalettes.value.indexOf(colorPalette);
    if (index !== -1) {
        colorPalettes.value.splice(index, 1);
    }
}

function addPallete(newPallete: { mid: string; start: string; end: string }) {
    colorPalettes.value.push(newPallete);
}

function clearColorPalettes() {
    colorPalettes.value = [];
}
</script>

<style scoped>
input[type="color"] {
    appearance: none;
    border: none;
    outline: none;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    cursor: pointer;
}

/* Optional: Style the color input value display */
input[type="color"]::-webkit-color-swatch {
    border: none;
    border-radius: 50%;
    padding: 0;
}

input[type="color"]::-webkit-color-swatch-wrapper {
    border: none;
    border-radius: 50%;
    padding: 0;
}
</style>
