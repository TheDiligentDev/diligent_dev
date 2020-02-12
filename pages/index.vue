<template>
  <div class="container">
    <b-row>
      <b-col class="mt-4" sm="12" md="4" lg="4" v-for="video in videos" :key="video.id.videoId">
        <div class="shadow bg-white rounded">
          <b-img :src="video.snippet.thumbnails.high.url" fluid-grow class="shadow" />
          <div class="pt-1 pr-3 pl-3 pb-1">
            <h4>{{video.snippet.title}}</h4>
            <p>{{video.snippet.description}}</p>
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
    console.log(process.env.YOUTUBE_API_KEY)
    const { data } = await axios.get(
      `https://www.googleapis.com/youtube/v3/search?key=${process.env.YOUTUBE_API_KEY}&channelId=UCLrTZVMYP_VsEyzxTAMcIcQ&part=snippet,id&order=date&maxResults=20`
    )

    let videos = data.items.filter(v => {
      return v.id.kind === 'youtube#video'
    })

    return {
      videos: videos
    }
  },
  methods: {}
}
</script>

<style>
</style>
