<template>
  <div class="container">
    <b-row>
      <b-col class="mt-4" sm="12" md="4" lg="4" v-for="video in videos" :key="video.id.videoId">
        <div class="shadow bg-white rounded">
          <a :href="'https://youtu.be/' + video.id.videoId" target="_blank">
            <b-img :src="video.snippet.thumbnails.high.url" fluid-grow class="shadow" />
          </a>
          <div class="pt-1 pr-3 pl-3 pb-1">
            <a :href="'https://youtu.be/' + video.id.videoId" target="_blank">
              <h4 class="video-title pb-1">{{video.snippet.title}}</h4>
            </a>
            <p>{{video.snippet.description}}</p>
          </div>
          <div class="text-center pb-4">
            <a :href="'https://youtu.be/' + video.id.videoId" target="_blank" class="btn btn-danger">
              Play on Youtube
            </a>
          </div>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://www.googleapis.com/youtube/v3/search?key=${process.env.YOUTUBE_API_KEY}&channelId=UCLrTZVMYP_VsEyzxTAMcIcQ&part=snippet,id&order=date&maxResults=20`
    )

    let videos = data.items.filter(v => {
      return v.id.kind === 'youtube#video'
    })

    console.log(videos)

    return {
      videos: videos
    }
  },
  methods: {}
}
</script>

<style>
.video-title {
  color: #dc3545;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; /* number of lines to show */
}

.video-title:hover {
  text-decoration: none;
  color: red;
}

a:hover, a:visited, a:link, a:active
{
    text-decoration: none;
}
</style>
