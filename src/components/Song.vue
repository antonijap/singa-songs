<template>
<div class="song">
    <img src="https://s3-eu-west-1.amazonaws.com/prod-ecs-service-image-api-media/media/images/modified/2/bfa822a0d0d83478f357193f20888df59fb945eaa6b407ef7b328d7e8f331801.jpg" alt="">
    <div class="meta">
        <span class="title">{{ title }}</span>
        <span class="title">{{ artist }}</span>
        <span class="genre">{{ genre }}</span>
    </div>
</div>
</template>

<script>
export default {
  name: 'Song',
  data () {
    return {
      title: 'Cry',
      artist: 'Pink',
      genre: 'pop'
    }
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
        }
    }   
</style>