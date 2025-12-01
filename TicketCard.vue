<template>
    <div class="ticket-card" :class="{ featured: tier.featured }">
        <div class="top-row">
            <h2>{{ tier.name }}</h2>
            <span class="fav" @click="$emit('favourite', tier.id)">
                {{ tier.favourite ? '❤️' : '🤍' }}
            </span>
        </div>

        <p class="price">R {{ tier.price }}</p>

        <ul>
            <li v-for="(b, i) in tier.benefits" :key="i">{{ b }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        tier: Object,             
    },        
};
</script>

<style>
.featured {
    border: 2px solid var(--featured);
    transform: scale(1.03);
}

.top-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.fav {
    cursor: pointer;
    font-size: 22px;
    transition: transform 2s ease;
}

.fav:hover {
    transform: scale(1.3);
}

.price {
    font-size: 24px;
    font-weight: bold;
    margin: 10px 0;
}
</style>