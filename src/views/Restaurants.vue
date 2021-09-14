<template>
  <div class="container py-5">
    <NavTabs />

    <!-- RestaurantsNavPills -->
    <RestaurantsNavPills :categories="categories" />
    <div class="row">
      <!-- RestaurantCard -->
      <RestaurantCard 
        v-for="restaurant in restaurants" 
        :key="restaurant.id" 
        :initialRestaurant="restaurant" 
      />
    </div>

    <!-- RestaurantsPagination -->
    <RestaurantsPagination 
      :current-page="currentPage"
      :total-page="totalPage"
      :previous-page="previousPage"
      :next-page="nextPage"
      :category-id="categoryId"
    />
  </div>
</template>

<script>
import NavTabs from './../components/NavTabs'
import RestaurantCard from './../components/RestaurantCard'
import RestaurantsNavPills from './../components/RestaurantsNavPills'
import RestaurantsPagination from './../components/RestaurantsPagination'


const dummyData = {
    "restaurants": [
        {
            "id": 4,
            "name": "Alfredo Leuschke Sr.",
            "tel": "246-072-7169 x21409",
            "address": "252 Farrell Hill",
            "opening_hours": "08:00",
            "description": "aut soluta et",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=63.48155690233037",
            "viewCounts": 35,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T18:56:49.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 5,
            "name": "Brice Bauch PhD",
            "tel": "(024) 826-6475",
            "address": "54700 Kihn Heights",
            "opening_hours": "08:00",
            "description": "et",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=49.91198923345017",
            "viewCounts": 4,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T18:04:20.000Z",
            "CategoryId": 1,
            "Category": {
                "id": 1,
                "name": "中式料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 6,
            "name": "Eve Corkery",
            "tel": "922-633-4075",
            "address": "669 Janie Cliffs",
            "opening_hours": "08:00",
            "description": "Qui unde eum amet libero.\nEt occaecati libero elig",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=23.52124987844537",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 1,
            "Category": {
                "id": 1,
                "name": "中式料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 7,
            "name": "Jovanny Quitzon",
            "tel": "500-605-6460",
            "address": "23593 Salvador Skyway",
            "opening_hours": "08:00",
            "description": "Et totam voluptatem nesciunt vel. Porro similique ",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=46.35997395193871",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": true,
            "isLiked": false
        },
        {
            "id": 8,
            "name": "Maude Dickinson",
            "tel": "893.214.2726 x34733",
            "address": "4996 Jordon Tunnel",
            "opening_hours": "08:00",
            "description": "qui inventore autem",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=30.088708477063285",
            "viewCounts": 4,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T19:02:01.000Z",
            "CategoryId": 2,
            "Category": {
                "id": 2,
                "name": "日本料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": true,
            "isLiked": false
        },
        {
            "id": 9,
            "name": "Alden Reinger",
            "tel": "036.805.0023 x1226",
            "address": "464 Ernesto Hill",
            "opening_hours": "08:00",
            "description": "Ipsam cumque nihil. Laborum est enim. Aut rerum ad",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=25.776533197006056",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 3,
            "Category": {
                "id": 3,
                "name": "義大利料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 10,
            "name": "Ryder Hintz",
            "tel": "(590) 232-2052",
            "address": "188 Loraine Crescent",
            "opening_hours": "08:00",
            "description": "Corporis et tenetur inventore ipsam ex libero ab n",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=30.676668227125358",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 5,
            "Category": {
                "id": 5,
                "name": "素食料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 11,
            "name": "Nat Altenwerth",
            "tel": "(781) 761-8520 x2731",
            "address": "803 Otho Fields",
            "opening_hours": "08:00",
            "description": "quisquam expedita magni",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=90.2625244386088",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 2,
            "Category": {
                "id": 2,
                "name": "日本料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 12,
            "name": "Diana Schaefer",
            "tel": "(084) 787-1373 x725",
            "address": "2059 Ledner Inlet",
            "opening_hours": "08:00",
            "description": "In repellat voluptas aut non qui. Voluptatem et ar",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=64.54266428046233",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 1,
            "Category": {
                "id": 1,
                "name": "中式料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": false
        },
        {
            "id": 13,
            "name": "Izabella Barrows",
            "tel": "692.671.8299 x416",
            "address": "45272 Jacey Stream",
            "opening_hours": "08:00",
            "description": "Et aut eius quae consequatur laborum soluta et.\nNi",
            "image": "https://loremflickr.com/320/240/restaurant,food/?random=29.28907805634793",
            "viewCounts": 0,
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z",
            "CategoryId": 4,
            "Category": {
                "id": 4,
                "name": "墨西哥料理",
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z"
            },
            "isFavorited": false,
            "isLiked": true
        }
    ],
    "categories": [
        {
            "id": 1,
            "name": "中式料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 2,
            "name": "日本料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 3,
            "name": "義大利料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 4,
            "name": "墨西哥料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 5,
            "name": "素食料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 6,
            "name": "美式料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        {
            "id": 7,
            "name": "複合式料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        }
    ],
    "categoryId": "",
    "page": 1,
    "totalPage": [
        1,
        2,
        3,
        4,
        5,
        6
    ],
    "prev": 1,
    "next": 2
}

export default {
  name: 'Restaurants',
  components: {
    NavTabs,
    RestaurantCard,
    RestaurantsNavPills,
    RestaurantsPagination
  },
  data () {
    return {
      restaurants: [],
      categories: [],
      categoryId: -1,
      currentPage: 1,
      totalPage: -1,
      previousPage: -1,
      nextPage: -1
    }
  },
  created() {
    this.fetchRestaurants()
  },
  methods: {
    fetchRestaurants() {
      const { restaurants, categories, categoryId, page, totalPage, prev, next } = dummyData
      this.restaurants = restaurants
      this.categories = categories
      this.categoryId = categoryId
      this.currentPage = page
      this.totalPage = totalPage
      this.previousPage = prev
      this.nextPage = next
    }
  }
}
</script>