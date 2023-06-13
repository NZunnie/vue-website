<template>
  <v-app id="home">
<!-- Include Header component -->
    <HeaderPage />
    <!--provides a fluid layout for the page content -->
    <v-container fluid>
      <div class="head mt-12">
    <!--displays a set of slides -->
    <v-carousel
    cycle color="grey-lighten-1" 
    height="520"
    hide-delimiter-background
    show-arrows="hover"
  >
<!-- Slide -->
      <v-carousel-item v-for="(slide, index) in slides" :key="index">
        <v-img :src="slide.image" :alt="slide.title" contain></v-img>
        <div class="slide-caption">
          <h1>{{ slide.title }}</h1>
          <p>{{ slide.description }}</p>
        </div>
      </v-carousel-item>
    </v-carousel>
  </div>

<!-- About Section -->
<v-col cols="12" class="mt-10 about-section" id="about" >
      <div>
        <v-row align-content="center">
          <v-col cols="12" md="6">
          <!-- Kimchi Image -->
            <div class="kimchi-image">
              <v-img src="@/assets/img/about.jpg" height="300" class="kimchi-img"></v-img>
        </div>
      </v-col>
      <v-col cols="12" md="6">
        <h1 class="mt-2 mb-4 text-orange-lighten-5" style="text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);">
          <strong>Kimchi</strong>
        </h1>
        <p class="text-gray-dark mt-3" style="font-size:18px">
          Kimchi is a Korean staple that has been around for centuries. It is a fermented vegetable dish that is made
          with cabbage, radish, and other vegetables. Kimchi is a healthy and delicious food that is packed with
          vitamins and minerals. It is also a good source of probiotics, which are beneficial for gut health. Kimchi
          is now a popular food all over the world and is a great way to experience Korean culture.
        </p>
          </v-col>
        </v-row>
      </div>
    </v-col>
  
<!-- Products Section -->
<div class="text-center mt-10 mb-10" id="products">
  <h1><strong>PRODUCTS</strong></h1>
</div>
    <v-col cols="12" class="imgHover">
      <v-row class="fill-height" align-content="center" justify="center">
      <!-- Product Item : Iterate over each product item in the items array using v-for-->
      <v-col cols="12" sm="6" md="4" 
      v-for="(item, i) in items" :key="i">
  
           <!-- Apply hover effect using v-hover -->
           <v-hover v-slot="{ isHovering, props }">
              <v-card
                :elevation="isHovering ? 12 : 2"
                :class="{ 'on-hover': isHovering }"
                v-bind="props"
              >
              <v-img :src="item.img" height="225px" cover></v-img>
              <v-card-title class="text-center text-deep-orange">{{ item.title }}</v-card-title>
                <div class="text-center">{{ item.price }}</div>
                <v-card-text>
                <div class="d-flex justify-center">
                  <v-btn small icon="fa-solid fa-cart-arrow-down" class="mr-10"></v-btn>
                  <v-btn small @click="showProductDetails(item)" class="bg-yellow-darken-2 text-center">
                    Details
                  </v-btn>
                </div>
                </v-card-text>
              
            </v-card>
            </v-hover>
          </v-col>
        
      </v-row>
    </v-col>

    <!-- Product Details Dialog -->
    <v-dialog v-model="dialog" max-width="500px">
        <v-card>
          <!-- Display the selected product title as the dialog title -->
          <v-card-title class="headline text-center text-deep-orange">{{ selectedProduct.title }}</v-card-title>
          <v-card-text>
            <div class="text-center">
              <v-img :src="selectedProduct.img" height="300px" contain></v-img>
            </div>
            <div class="text-center mt-4">{{ selectedProduct.price }}</div>
            <div class="text-center mt-2">{{ selectedProduct.description }}</div>
          </v-card-text>
          <v-card-actions class="justify-center">
            <!-- Close the dialog when the "Close" button is clicked -->
            <v-btn text @click="dialog = false"  class="bg-yellow-darken-2">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>


<!-- Review Section -->
<v-col cols="12" class="mt-16 review-section" id="reviews">
    <v-section id="reviews" class="my-10">
      <v-container>
        <h1 class="text-center"><strong>Reviews</strong></h1>
        <v-row justify="center" align-content="center" class="mt-6">
          <!-- Iterate over each review in the reviews array using v-for -->
          <v-col cols="12" sm="4" md="4" v-for="(review, index) in reviews" :key="index">
            <v-card class="mx-auto review-card" max-width="344">
              <!-- Display the review -->
              <v-img :src="review.image" height="200px" cover></v-img>
              <v-card-title class="review-title">{{ review.title }}</v-card-title>
              <v-card-subtitle class="review-subtitle">{{ review.date }}  ---  {{ review.userID }}</v-card-subtitle>
              <v-row class="d-flex align-center mt-2 mb-1 mr-5">
              <!-- Display the review rating using v-rating -->
                <v-rating
                v-model="review.rating"
                :size="28"
                background-color="transparent"
                color="#FFC107"
                readonly
                :dense="true"
                class="mx-auto"
                ></v-rating>
                <span class="ml-2">{{ `(${review.rating})` }}</span> <!-- 숫자를 (rating 숫자) 형태로 표시 -->
              </v-row>
                <v-card-text>{{ review.description }}</v-card-text>
              </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-section>
  </v-col>


  </v-container>
<!-- Footer component -->
  <FooterView />
  </v-app>
</template>

<script>
 // Importing components
import HeaderPage from "../components/HeaderPage.vue";
import FooterView from "../components/FooterView.vue";

export default {
  name: "HomeView",
  components: { // Registering components
    HeaderPage,
    FooterView,
  },
  data() {
    return {
      /* Head slides data */
      slides: [
        {
          image: require("@/assets/img/pop1.jpg"),
          title: "Delicious Kimchi",
          description: "Experience the authentic taste of traditional kimchi."
        },
        {
          image: require("@/assets/img/pop2.jpg"),
          title: "Healthy and Nutritious",
          description: "Discover the health benefits of our fresh kimchi products."
        },
        {
          image: require("@/assets/img/pop3.jpg"),
          title: "Variety of Flavors",
          description: "Explore a wide range of kimchi flavors to suit your palate."
        }
      ], 
      /* Product Item data*/
      items: [
        {
          img: require("@/assets/img/pd1.jpg"),
          title: "Cabbage Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
        {
          img: require("@/assets/img/pd2.jpg"),
          title: "Radish Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
        {
          img: require("@/assets/img/pd3.jpg"),
          title: "Cucumber Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
        {
          img: require("@/assets/img/pd4.jpg"),
          title: "Non-spicy Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
        {
          img: require("@/assets/img/pd5.jpg"),
          title: "Vegan Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
        {
          img: require("@/assets/img/pd6.jpg"),
          title: "Altarie Kimchi",
          price:"$10/kg",
          description: "Ingredients: Napa cabbage, Daikon radish, Rice paste, Red chili powder, Salt, Coriander, Lactic acid bacteria",
        },
      ],
      /* Reviews data*/
      reviews: [
        {
          image: require("@/assets/img/re1.jpg"),
          title: "Super delicious",
          userID: "kimchiman",
          date: "01 Jun 2022",
          rating: 4.5,
          description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit rem saepe sapiente deleniti, odio non laborum fuga."
        },
        {
          image: require("@/assets/img/re2.jpg"),
          title: "the best kimchi jjigae",
          userID: "yummy",
          date: "21 Jan 2023",
          rating: 4.8,
          description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit rem saepe sapiente deleniti, odio non laborum fuga."
        },
        {
          image: require("@/assets/img/re3.jpg"),
          title: "BBQ with kimchi",
          userID: "BBQ king",
          date: "31 May 2023",
          rating: 5.0,
          description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit rem saepe sapiente deleniti, odio non laborum fuga."
        }
      ],
      /* Dialog data */
      dialog: false, // control the visibility of the dialog
      selectedProduct: null,
    };
  },
  methods: {
    //Set up the selected product and open the dialog
    showProductDetails(product) {
      this.selectedProduct = product;
      this.dialog = true;
    },
  },
};
</script>

<style scoped>
.head {
  position: relative;
  height: 500px;
}
.slide-caption {
  position: absolute;
  top: 80%;
  left: 45%;
  transform: translate(-50%, -50%);
}

.slide-caption h1 {
  font-size: 36px;
  margin-bottom: 16px;
}

.kimchi-image {
  display: flex;
  justify-content: center;
}

#about {
  padding:3% 10%;
}
.about-section {
    background-image: url('~@/assets/img/bgimg6.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    overflow: hidden;
  }
.on-hover {
  transform: translateY(-10px);
  transition: transform 0.3s ease;
}
.imgHover v-card-title {
  font-size: 20px;
  font-weight: bold;
}

.imgHover {
  padding: 0 15%;
}
#reviews {
  width: 100%;
  height: auto;
  text-align: center;
}
.review-section {
    background-image: url('~@/assets/img/bgimg5.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    overflow: hidden;
  }
</style>