<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
            <VideoDetail :video="selectedVideo"></VideoDetail>
        </div>
    </div>
</template>

<script>
import SearchBar from "./components/SearchBar"
import VideoList from "./components/VideoList"
import VideoDetail from "./components/VideoDetail"
import axios from 'axios'
const API_KEY = 'AIzaSyC1UfAuWRUzj1ryFCXIc6XBERsdg6knNnE'

export default {
name: 'App',
components: {
    SearchBar,
    VideoList,
    VideoDetail
}, 
data() {
return {
    videos: [],
    selectedVideo: null
}
},
methods: {
    onTermChange(searchTerm) {
        axios.get('https://www.googleapis.com/youtube/v3/search', {
            headers: {'Access-Control-Allow-Origin': '*'},
            dataType: 'jsonp',
            params: {
                key: API_KEY, 
                type: 'video', 
                part: 'snippet',
                q: searchTerm
            }
        }).then(response => this.videos = response.data.items)
    },
    onVideoSelect(video) {
        this.selectedVideo = video
    }
}

}
</script>

<style>
</style>
