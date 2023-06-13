<template>
<div>
  <!-- The navigation bar -->
  <v-app-bar app color="#FCBD19" dark class="px-4">
    <!-- Toggle button for the navigation drawer -->
    <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    <v-toolbar-title>
      <a class="navbar-brand" href="/">
        <img :src="require('@/assets/img/logo.png')"  alt="LBK" class="logo-image">
      </a>
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <!-- Navigation items (hidden on small screens) -->
    <v-app-bar-items class="hidden-sm-and-down">
      <v-btn text @click="scroll('home')" :class="{ 'text-gray': activeSection === 'home' }">Home</v-btn>
      <v-btn text @click="scroll('about')" :class="{ 'text-gray': activeSection === 'about' }">Kimchi</v-btn>
      <v-btn text @click="scroll('products')" :class="{ 'text-gray': activeSection === 'products' }">Products</v-btn>
      <v-btn text @click="scroll('reviews')" :class="{ 'ttext-gray': activeSection === 'reviews' }">Reviews</v-btn>
      <v-btn text @click="goToPage('cart')">Cart</v-btn>
      <v-btn text @click="goToPage('checkout')">Checkout</v-btn>
      <v-btn text @click="scroll('contact')" :class="{ 'text-gray': activeSection === 'contact' }">Contact</v-btn>
    </v-app-bar-items>
  </v-app-bar>

  <!-- The navigation drawer -->
  <v-navigation-drawer v-model="drawer" temporary app 
  class="bg-yellow-darken-4">
    <v-list dense >
      <v-list-item v-for="item in menuItems" :key="item.title" @click="scroll(item.section)">
        <v-list-item-title>{{ item.title }}</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</div>
</template>

<script>
export default {
  data() {
    return {
      drawer: false, // Flag to control the visibility of the navigation drawer
      activeSection: '', // Currently active section
      menuItems: [
        { title: 'Home', section: 'home' },
        { title: 'Kimchi', section: 'about' },
        { title: 'Products', section: 'products' },
        { title: 'Reviews', section: 'reviews' },
        { title: 'Cart', section: 'cart' },
        { title: 'Checkout', section: 'checkout' },
        { title: 'Contact', section: 'contact' },
      ],// Array of menu items
    };
  },
  methods: {
    scroll(refName) {
    const element = document.getElementById(refName);
    if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
    this.activeSection = refName; // Set the active section
    this.drawer = false; // Close the navigation drawer after clicking a menu item
  }
},
    goToPage(page) { // Navigate to the specified page
     if (page === 'cart') {
    this.$router.push('/cart'); // Replace '/cart' with the actual route for the CartView component
  } else if (page === 'checkout') {
    this.$router.push('/checkout'); // Replace '/checkout' with the actual route for the CheckoutView component
  }
      this.drawer = false; 
    },
  },
};
</script>

<style scoped>
.logo-image {
  width: 110px;
  height: auto;
}


/* Hide the navigation items on small screens */
@media (max-width: 959.98px) {
  .hidden-sm-and-down {
    display: none;
  }
}
</style>