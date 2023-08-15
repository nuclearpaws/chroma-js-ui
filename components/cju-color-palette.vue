<template>
    <div class="color-palette">
        <button
            v-for="color in colors"
            v-bind:key="color"
            title="Copy to Clipboard"
            class="color-palette-item"
            v-on:click="copyToClipboardAsync(color)"
        >
            <div v-bind:style="{ background: color }" class="color-box"></div>
            <code>{{ color }}</code>
        </button>
    </div>
</template>

<script lang="ts" setup>
interface Props {
    colors: string[];
}

const props = defineProps<Props>();

async function copyToClipboardAsync(textToCopy: string): Promise<void> {
    try {
        await navigator.clipboard.writeText(textToCopy);
    } catch (err) {
        console.error(err);
    }
}
</script>

<style scoped>
button {
    padding: 0px 0px 5px 0px;
    border-radius: 10px;
}

button:hover {
    background-color: darkgray;
}

button:active {
    background-color: black;
    color: white;
}

.color-palette {
    display: flex;
    grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
    gap: 5px;
}

.color-palette-item {
    border: 0;
    flex-grow: 1;
}

.color-box {
    aspect-ratio: 1/1;
    border-radius: 8px;
}
</style>
