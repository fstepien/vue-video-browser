<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <VideoList :videos="videos"></VideoList>
    </div>
</template>

<script>
import SearchBar from "./components/SearchBar"
import VideoList from "./components/VideoList"
import axios from 'axios'
const API_KEY = 'AIzaSyC1UfAuWRUzj1ryFCXIc6XBERsdg6knNnE'

export default {
name: 'App',
components: {
    SearchBar,
    VideoList
}, 
data() {
return {
    videos: []
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
    }
}

}
</script>

<style>
</style>
