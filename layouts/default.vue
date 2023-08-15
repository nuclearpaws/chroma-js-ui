<template>
    <div class="wrapper">
        <header>
            <h1>Chroma JS - UI</h1>
        </header>
        <nav>
            <ul>
                <li><nuxt-link to="/">Home</nuxt-link></li>
                <li><nuxt-link to="/tool">Tool</nuxt-link></li>
            </ul>
        </nav>
        <main>
            <div class="container">
                <slot />
            </div>
        </main>
        <footer>
            <p>&copy; 2023 Chroma JS UI. All rights reserved.</p>
        </footer>
    </div>
</template>

<script lang="ts" setup></script>

<style scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 20px;
    flex: 1;
}
</style>
