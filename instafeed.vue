<template>
  <div class="wrapper">
    <div class="posts">
      <div class="thumb-box" v-for="post in posts" :key="post.id" @click="goToPost(post.link)">
        <img class="thumbnail-image" :src="post.images.low_resolution.url">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    // Instagram API Access Token
    access_token: {
      type: String,
      required: true
    },

    // Number of posts to return
    numPosts: {
      type: String,
      required: false,
      default: "10"
    },

    // Only display images with 1x1 aspect ratio
    squareOnly: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data() {
    return {
      base_url: "https://api.instagram.com/v1/users/self/media/recent/?",
      posts: []
    };
  },
  methods: {
    async getInstaFeed() {
      const res = await this.$axios.$get(this.endpoint);
      if (!this.squareOnly) {
        this.posts = res.data;
      } else {
        this.getSquarePosts(res.data);
      }
    },
    getSquarePosts(postData) {
      postData.forEach(post => {
        if (
          post.images.low_resolution.height === post.images.low_resolution.width
        ) {
          this.posts.push(post);
        }
      });
    },
    goToPost(url) {
      window.open(url, "_blank");
    }
  },
  mounted() {
    this.getInstaFeed();
  },
  computed: {
    // Returns Instagram API request url including access token from ENV
    endpoint() {
      return this.base_url + this.count + "&access_token=" + this.access_token;
    }
  }
};
</script>

<style lang="scss" scoped>
.posts {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: 100%;
  grid-gap: 10px;
  > img {
    object-fit: cover;
    width: 100%;
    max-height: 100%;
  }
}
a {
  text-decoration: none;
}
.thumb-box {
  overflow: hidden;
}
.thumbnail-image {
  display: inline-block;
  vertical-align: middle;
  width: 100%;
  &:hover {
    cursor: pointer;
    transition: all 0.3s ease;
    transform: scale(1.05);
    opacity: 0.7;
  }
}
</style>