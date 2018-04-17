<template>
<div class="song">
    <img :src="image" alt="">
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
        img {
            width: 100%;
            height: auto;
            border-radius: 4px;
        }
        .meta {
            padding: 8px 0;
            .title {
                font-weight: 600;
                display: block;
            }
            .artist {
                font-weight: 500;
                display: block;
            }
            .genre {
                color: #333333;
                font-size: 12px;
                text-transform: uppercase;
                display: block;
                font-weight: 600;
            }
        }
    }   
</style>