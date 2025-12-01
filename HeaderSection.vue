<template>
    <header class="header">
        <h1>Food Fest 2025</h1>
        <p>Choose your ticket tier and get ready for an unforgettable culinary experience!</p>

        <button class="dark-toggle" @click="$emit('toggle-dark')">
            {{ darkMode ? '☀️ Light Mode' : '🌙 Dark Mode' }}
        </button>
    </header>
</template>

<script>
export default {
    props: {
        darkMode: Boolean
    },
};
</script>

<style>
.header {
    text-align: center;
    padding: 40px 20px;
}

.dark-toggle {
    margin-top: 10px;
    padding: 10px 20px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background: var(--featured);
    color: #000;
    font-weight: bold;
}
</style>