<template>
  <v-footer class="footer">
    <v-container>
      <v-row class="footer-content" align="center">
        <v-col cols="12" md="6">
          <div class="footer-contact">
            <h1 class="mb-5">Contact Us</h1>
            <div class="footer-contact-info">
              <i class="fas fa-envelope"></i>
              <p class="footer-contact-text">Email: info@kcentre.org.nz</p>
            </div>
            <div class="footer-contact-info">
              <i class="fas fa-phone"></i>
              <p class="footer-contact-text">Phone: 021 771 798</p>
            </div>
            <div class="footer-contact-info">
              <i class="fas fa-map-marker-alt"></i>
              <p class="footer-contact-text">5 Kingsford Mews, Hamilton East, Hamilton, New Zealand</p>
            </div>
          </div>
        </v-col>
        <v-col cols="12" md="6">
          <div class="footer-subscribe">
            <h2 class="mb-5 text-orange-darken-3">Get 10% off your first order</h2>
            <v-form class="footer-form" @submit.prevent="submitForm">
              <v-row no-gutters align="center" >
                <v-col cols="12" sm="9">
                  <v-text-field v-model="email" label="Enter your email" required></v-text-field>
                </v-col>
                <v-col cols="12" sm="3">
                  <v-btn type="submit" class="bg-yellow darken-2 ml-5">Submit</v-btn>
                </v-col>
                <v-col cols="12">
          <div class="footer-social">
            <a href="https://www.instagram.com" class="footer-social-link mr-5">
              <i class="fab fa-instagram fa-xl"></i>
            </a>
            <a href="https://www.facebook.com" class="footer-social-link mr-5">
              <i class="fab fa-facebook fa-xl"></i>
            </a>
            <a href="https://www.youtube.com" class="footer-social-link mr-5">
              <i class="fab fa-youtube fa-xl"></i>
            </a>
          </div>
        </v-col>
              </v-row>
            </v-form>
          </div>
        </v-col>
      </v-row>
      <v-row >
        <v-col cols="12" class="mt-5" >
          <p>
            © 2023 Live Better KCentre Kimchi. All Rights Reserved.
          </p>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<script>
export default {
  name: 'FooterView',
  data() {
    return {
      email: '',
    };
  },
  methods: {
    submitForm() {
     //Later...
    },
  },
};
</script>

<style scoped>
.footer {
  background-color: #212121;
  color: #ffffff;
  padding: 20px 0;
  font-size: 14px;
  text-align: center;
}

.footer-content {
  flex-wrap: wrap;
  justify-content: center;
}

.footer-contact {
  text-align: left;
}

.footer-contact-info {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.footer-contact-text {
  margin-left: 10px;
}

.footer-subscribe {
  text-align: left;
  margin-top: 20px;
}


.footer-social-link {
  color: #ffffff;
  font-size: 20px;
  margin-right: 10px;
}


</style>


