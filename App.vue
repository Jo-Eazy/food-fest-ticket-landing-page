<template>
  <div class="container">
    <HeaderSection :darkMode="darkMode" @toggle-dark="toggleDarkMode" />

    <transition-group name="fade" tag="div" class="ticket-grid">
      <TicketCard
        v-for="tier in tiers"
        :key="tier.id"
        :tier="tier"
        :favourited="favourites.includes(tier.id)"
        @toggle-favourite="toggleFavourite"
      />
    </transition-group>
  </div>
</template>

<script setup>
import TicketCard from './components/TicketCard.vue'
import HeaderSection from './components/HeaderSection.vue'

export default {
  name: 'App',
  components: { HeaderSection, TicketCard },
  data() {
    return {
      darkMode: false,
      favourites: JSON.parse(localStorage.getItem('ff-faves') || '[]'),

      tiers: [
        { id: 1, name: 'Standard Pass', price: 299, featured: false, benefits: ['Access to general food stalls', 'Free welcome drink', 'Live music area access'] },
        { id: 2, name: 'VIP Experience', price: 799, featured: true, benefits: ['All Standard benefits', 'VIP lounge', 'Exclusive chef tasting menu', 'Priority entry'] },
        { id: 3, name: 'Family Bundle', price: 999, featured: false, benefits: ['4 Standard Passes', 'Kids play area access', 'Discounted merchandise'] },
      ],
    };
  },
  mounted() {
    const savedMode = localStorage.getItem("darkMode");
    this.darkMode = savedMode === "true";
    document.documentElement.classList.toggle("dark", this.darkMode);
  },

  methods: {
    toggleFavourite(id) {
      const index = this.favourites.indexOf(id)
      if (index === -1) {
        this.favourites.push(id)
      } else {
        this.favourites.splice(index, 1)
      }
      localStorage.setItem('ff-faves', JSON.stringify(this.favourites))
    },
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
      document.documentElement.classList.toggle("dark", this.darkMode);
      localStorage.setItem("darkMode", this.darkMode);
    },
  },
};
</script>

<style>
.ticket-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 20px;
  padding: 30px;
}
</style>
