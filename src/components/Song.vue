<template>
<div class="song">
    <img style="width: 250px; height: 250px;" :src="image" alt="">
    <div class="meta">
        <span class="title">{{ title }}</span>
        <span class="title">{{ artist }}</span>
        <span class="genre">{{ genre }}</span>
    </div>
</div>
</template>

<script>
export default {
  name: 'SongList',
  //the props property is given in the parent component, it enables passing down dynamic data for the child component
  props: {
    title: {
        type: String,
        required: true
    },
    artist: {
        type: String,
        required: true
    },
    image: {
        type: String,
        required: true
    },
    genre: {
        type: String,
        required: true
    },
  }
}
</script>

<style lang="scss" scoped>
    .song {
        background: black;
        color: white;
        .meta {
            padding: 8px;
            .title {
                font-size: 16px;
                letter-spacing: -0.2px;
                font-family: "Basier";
                font-weight: 600;
                display: block;
            }
            .artist {
                font-size: 16px;
                letter-spacing: -0.2px;
                font-family: "Basier";
                font-weight: 500;
                display: block;
            }
            .genre {
                color: #333333;
                font-size: 12px;
                letter-spacing: -0.2px;
                text-transform: uppercase;
                display: block;
                font-family: "Basier";
                font-weight: 600;
            }
            .song-image {
                width: 500px;
                height: 500px;
                
            }
        }
    }   
</style>