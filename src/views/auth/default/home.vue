<template>
  <div class="card-container">
    <!-- <p v-t="'student_management'"></p> -->

    <!-- {{ homeData }} -->

    <!-- <Card v-for="card in homeData" :key="card.id" :title="card.name_en" :description="card.description" /> -->

    <b-row>
      <template v-for="(card, index) in homeData" :key="index">
        <b-col xl="4">
          <b-card>
            <div class="d-flex justify-content-between align-items-center">
              <div>
                <div class="p-3 rounded bg-soft-primary">
                  <svg width="30" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M11.997 15.1746C7.684 15.1746 4 15.8546 4 18.5746C4 21.2956 7.661 21.9996 11.997 21.9996C16.31 21.9996 19.994 21.3206 19.994 18.5996C19.994 15.8786 16.334 15.1746 11.997 15.1746Z" fill="currentColor"></path>
                    <path opacity="0.4" d="M11.9971 12.5838C14.9351 12.5838 17.2891 10.2288 17.2891 7.29176C17.2891 4.35476 14.9351 1.99976 11.9971 1.99976C9.06008 1.99976 6.70508 4.35476 6.70508 7.29176C6.70508 10.2288 9.06008 12.5838 11.9971 12.5838Z" fill="currentColor"></path>
                  </svg>
                </div>
              </div>
              <div style="text-align: left;">
                <!-- <h1>{{ card.name_en }}</h1> -->
                <button type="button" class="btn btn-sm" @click="goDashboard"> <h3>{{ card.name_en }}</h3> </button>
                <p class="mb-0"> {{ card.description }} </p>
              </div>
            </div>
          </b-card>
        </b-col>
      </template>

    </b-row>
  </div>
</template>

<script>
// import Card from "@/components/common/Card.vue"
import axios from 'axios'
import { commonServiceBaseURL } from '@/config/api_config.js'

export default {
  name: 'HomePage',
  components: {
    // Card
  },
  data() {
    return {
      homeData: {},
      cards: [
        { id: 1, title: 'student_management', description:  "This is the student management description." },
        { id: 2, title: 'teacher_management', description: "This is the description for teacher management." },
        { id: 3, title: 'parent_management', description: "This is the description for parent management." },
        { id: 4, title: 'class_management', description: "This is the description for class management." },
        { id: 5, title: 'section_management', description: "This is the description for section management." },
      ],
    };
  },
  created() {
    console.log('HomePage created');
    this.loadData()
  },
  methods: {
    async loadData() {
        // Make the API call using Axios
        axios.get(commonServiceBaseURL + '/get-components')
        .then(response => {
          // Handle the successful response
          this.homeData = response.data;
        })
        .catch(error => {
          // Handle errors from the API
          console.error('Failed to fetch data:', error);
        });
    },
    goDashboard () {
      this.$router.push('/dashboard')
    }
  }
}
</script>

<style scoped>
.card-container {
  margin-top: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  /* display: grid; */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
</style>
