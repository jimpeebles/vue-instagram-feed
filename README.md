# vue-instagram-feed

Retrieves and displays the latest Instagram posts from an authenticated user

## Usage

You'll need an API token from Instagram to access your feed, which can be acquired [here](https://www.instagram.com/developer/authentication/).

## Props

```javascript
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

// Choose resolution - 'low_resolution' (320x320), 'standard_resolution' (640x640), 'thumbnail' (150x150)
resolution: {
    type: String,
    required: false,
    default: "low_resolution"
},

//Choose number of columns for grid
columns: {
    type: String,
    required: false,
    default: "3"
}
```
