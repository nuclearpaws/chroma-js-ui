<template>
    <div>
        <label v-bind:for="id">{{ name }}:</label>
        <div class="hex-container">
            <input
                type="text"
                v-bind:id="id"
                class="hex-input"
                v-model="value"
            />
            <input
                v-model="value"
                v-bind:style="{ backgroundColor: value }"
                type="color"
                class="color-preview"
            />
        </div>
    </div>
</template>

<script lang="ts" setup>
interface Props {
    id: string;
    name: string;
    value: string;
}

const props = defineProps<Props>();
const emit = defineEmits(["update:value"]);

const value = computed({
    get: () => props.value,
    set: (v) => {
        const regex = /^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/;
        if (regex.test(v)) {
            emit("update:value", v);
        }
    },
});
</script>

<style scoped>
.color-picker {
    border: 0;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.hex-container {
    display: flex;
    align-items: center;
    gap: 10px;
}

.hex-input {
    width: 100%;
    padding: 6px;
    font-size: 14px;
}

input[type="color"] {
    appearance: none;
    border: none;
    outline: none;
    cursor: pointer;
}

input[type="color"]::-webkit-color-swatch {
    border: none;
    padding: 0;
}

input[type="color"]::-webkit-color-swatch-wrapper {
    border: none;
    padding: 0;
}

.color-preview {
    width: 20px;
    height: 20px;
    border-radius: 4px;
}

input[type="color"] {
    border: none;
    border-radius: 8px;
    width: 30px;
    height: 30px;
    cursor: pointer;
}
</style>
