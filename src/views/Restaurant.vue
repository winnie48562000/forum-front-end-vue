<template>
  <div class="container py-5">
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantDetail 
      :initialRestaurant="restaurant" 
    />
    <hr>
    <!-- 餐廳評論 RestaurantComments -->
    <RestaurantComments
      :restaurant-comments="restaurantComments"
      @after-delete-comment="afterDeleteComment"
    />
    <!-- 新增評論 CreateComment -->
    <CreateComment
      :restaurant-id="restaurant.id"
      @after-create-comment="afterCreatComment"
    />
  </div>
</template>

<script>
import RestaurantDetail from './../components/RestaurantDetail'
import RestaurantComments from './../components/RestaurantComments'
import CreateComment from './../components/CreateComment'


const dummyData = {
    "restaurant": {
        "id": 13,
        "name": "Izabella Barrows",
        "tel": "692.671.8299 x416",
        "address": "45272 Jacey Stream",
        "opening_hours": "08:00",
        "description": "Et aut eius quae consequatur laborum soluta et.\nNisi aut voluptatem vel non at quas.\nCorrupti eum eum est aspernatur beatae soluta ea eos.\nHic qui eveniet voluptate temporibus voluptate sed.",
        "image": "https://loremflickr.com/320/240/restaurant,food/?random=29.28907805634793",
        "viewCounts": 4,
        "createdAt": "2021-09-08T08:34:40.000Z",
        "updatedAt": "2021-09-24T05:51:54.240Z",
        "CategoryId": 4,
        "Category": {
            "id": 4,
            "name": "墨西哥料理",
            "createdAt": "2021-09-08T08:34:40.000Z",
            "updatedAt": "2021-09-08T08:34:40.000Z"
        },
        "FavoritedUsers": [],
        "LikedUsers": [],
        "Comments": [
            {
                "id": 13,
                "text": "Consectetur atque sapiente officia doloremque qui fugiat.",
                "UserId": 2,
                "RestaurantId": 13,
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z",
                "User": {
                    "id": 2,
                    "name": "user1",
                    "email": "user1@example.com",
                    "password": "$2a$10$yVu0LNTtgpIx.ehwX6n/L.jJXKKnyE6AWdqsPdLV4.JvegiDZFtpK",
                    "isAdmin": false,
                    "image": null,
                    "createdAt": "2021-09-08T08:34:40.000Z",
                    "updatedAt": "2021-09-15T02:53:32.000Z"
                }
            },
            {
                "id": 63,
                "text": "Eos velit doloremque nobis et dignissimos quaerat molestias.",
                "UserId": 1,
                "RestaurantId": 13,
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z",
                "User": {
                    "id": 1,
                    "name": "root",
                    "email": "root@example.com",
                    "password": "$2a$10$PM9K3ZslTQWzH3zTNX7JqOD9m5SmUR5eNfDRx6TV2Ujrbgr.7ie.a",
                    "isAdmin": true,
                    "image": null,
                    "createdAt": "2021-09-08T08:34:40.000Z",
                    "updatedAt": "2021-09-08T08:34:40.000Z"
                }
            },
            {
                "id": 113,
                "text": "Dicta perspiciatis soluta.",
                "UserId": 3,
                "RestaurantId": 13,
                "createdAt": "2021-09-08T08:34:40.000Z",
                "updatedAt": "2021-09-08T08:34:40.000Z",
                "User": {
                    "id": 3,
                    "name": "user2",
                    "email": "user2@example.com",
                    "password": "$2a$10$6VAzzV4YdId/.jquKOOC8e32tdc6k/VgZfJPCCxwgMl/xAe39UXXW",
                    "isAdmin": false,
                    "image": null,
                    "createdAt": "2021-09-08T08:34:40.000Z",
                    "updatedAt": "2021-09-08T08:34:40.000Z"
                }
            }
        ]
    },
    "isFavorited": false,
    "isLiked": false
}

const dummyUser = {
  currentUser: {
    "id": 1,
    "name": "root",
    "email": "root@example.com",
    "image": null,
    "isAdmin": true
  },
  isAuthenticated: true
}

export default {
  name: 'Restaurant',
  components: {
    RestaurantDetail,
    RestaurantComments,
    CreateComment
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: '',
        categoryName: '',
        image: '',
        openingHours: '',
        tel: '',
        address: '',
        description: '',
        isFavorited: false,
        isLiked: false
      },
      restaurantComments: [],
      currentUser: dummyUser.currentUser
    }
  },
  created() {
    const { id } = this.$route.params
    this.fetchRestaurant(id)
  },
  methods: {
    fetchRestaurant () {
      const { restaurant, isFavorited, isLiked } = dummyData
      const {
        id,
        name,
        Category,
        image,
        opening_hours: openingHours,
        tel,
        address,
        description,
        Comments
      } = restaurant

      this.restaurant = {
        id,
        name,
        CategoryName: Category ? Category.name : '未分類',
        image,
        openingHours,
        tel,
        address,
        description,
        isFavorited,
        isLiked
      }

      this.restaurantComments = Comments
    },
    afterDeleteComment(commentId) {
      this.restaurantComments = this.restaurantComments.filter(
        comment => comment.id !== commentId
      )
    },
    afterCreatComment(payload) {
      const { commentId, restaurantId, text } = payload
      this.restaurantComments.push({
        id: commentId,
        RestaurantId: restaurantId,
        User: {
          id: this.currentUser.id,
          name: this.currentUser.name
        },
        text,
        createdAt: new Date()
      })
    }
  }
}
</script>
