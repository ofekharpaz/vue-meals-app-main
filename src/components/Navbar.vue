<template>
  <header class="header">
    <router-link :to="{ name: 'home' }" class="logo">Home</router-link>
    <nav class="nav-links">
      <router-link :to="{ name: 'byName' }" class="nav-link">Search Meals</router-link>
      <router-link :to="{ name: 'byLetter' }" class="nav-link">Meals By Letter</router-link>
      <router-link :to="{ name: 'ingredients' }" class="nav-link">Meals By Ingredients</router-link>
    </nav>
    <button class="burger-menu" @click="toggleNav">
      <div v-if="!isNavOpen">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <div v-else>
        <button class="close-button">&times;</button>
        <nav class="nav-links-open">
        <router-link :to="{ name: 'byName' }" class="nav-link">Search Meals</router-link>
        <router-link :to="{ name: 'byLetter' }" class="nav-link">Meals By Letter</router-link>
        <router-link :to="{ name: 'ingredients' }" class="nav-link">Meals By Ingredients</router-link>
      </nav>
      </div>
    </button>
  </header>
</template>

<script>
import { ref } from 'vue'; // Import ref for reactive properties

export default {
  setup() {
    const isNavOpen = ref(false); // Reactive property for nav open/close state
    
    const toggleNav = () => {
      isNavOpen.value = !isNavOpen.value; // Toggle the state of isNavOpen
    };

    return {
      isNavOpen,
      toggleNav
    };
  }
};
</script>




<style scoped>
  /* Reusable styles */
.nav-link {
  display: inline-flex;
  align-items: center;
  padding: 10px 20px;
  text-decoration: none;
  color: #333;
  transition: background-color 0.3s, color 0.3s;
}

.nav-link:hover {
  background-color: #ff9800; /* Orange color */
  color: #ffffff; /* White text */
}

/* Specific styles for the header */
.header {
  background-color: #ffffff; /* White background */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Shadow */
  height: 4rem; /* 16px multiplied by 4 (default font size) */
  display: flex;
  justify-content: space-between; /* Items spread out */
  align-items: center; /* Items centered */
  padding: 0 20px;
}

.logo {
  color: #ff9800; /* Orange color */
  font-weight: bold;
  text-decoration: none;
}

.burger-menu {
  display: none; /* Initially hide the burger menu */
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px;
}

.burger-menu span {
  display: block;
  width: 25px;
  height: 3px;
  background-color: #333;
  margin: 5px 0;
  transition: transform 0.3s, opacity 0.3s;
}

/* Open state of the nav links */
.nav-links-open {
  display: flex;
  flex-direction: column;
  position: absolute;
  top: 4rem; /* Height of the header */
  right: 0;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: auto;
  z-index: 10; /* Ensure it overlays other content */
}

.nav-links-open .nav-link {
  width: 100%;
  text-align: center;
}

.nav-links-open .nav-link:hover {
  background-color: #ff9800; /* Orange color */
  color: #ffffff; /* White text */
}

@media (max-width: 768px) {
  .nav-links {
    display: none; /* Hide the nav links by default on small screens */
  }

  .burger-menu {
    display: block; /* Show the burger menu button on small screens */
  }
}

.close-button {
  position: absolute;
  top: 0px;
  right: 25px;
  background-color: transparent;
  border: none;
  font-size: 40px; /* Increased font size */
  padding: 8px; /* Increased padding around the X */
  line-height: 1; /* Ensure the X is vertically centered */
  cursor: pointer;
  outline: none;
}

.close-button:hover {
  color: #666;
}
</style>