<template>
    <div v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="10">
        <h5>Latest Uploads</h5>

        <div class="row">
            <div v-for="(song, index) in songs" :key="'song-card-' + index">
                <song-card
                    :id=song.id
                    :name=song.name
                    :artist=song.artist
                    :album=song.album
                    :genre=song.genre
                    :year=song.year
                    :charter=song.charter
                    :length=song.length
                    :diffGuitar=song.diff_guitar
                    :diffBass=song.diff_bass
                    :diffRhythm=song.diff_rhythm
                    :diffDrums=song.diff_drums
                    :diffKeys=song.diff_keys
                    :diffGuitarghl=song.diff_guitarghl
                    :diffBassghl=song.diff_bassghl
                    :isPack=song.isPack
                    :hasForced=song.hasForced
                    :hasOpen=song.hasOpen
                    :hasTap=song.hasTap
                    :hasSections=song.hasSections
                    :hasStarPower=song.hasStarPower
                    :hasSoloSections=song.hasSoloSections
                    :hasVideo=song.hasVideo
                    :hasLyrics=song.hasLyrics
                    :hasNoAudio=song.hasNoAudio
                    :isFolder=song.isFolder
                    :hasBrokenNotes=song.hasBrokenNotes
                    :hasBackground=song.hasBackground
                    :noteCounts=song.noteCounts
                    :lastModified=song.lastModified
                    :uploadedAt=song.uploadedAt
                    :link=song.link
                    :directLinks=song.directLinks
                    :sources=song.sources
                    :hashes=song.hashes
                />
            </div>
        </div>
        <div class="row">
            <div class="loader scale-transition scale-out">
                <div class="preloader-wrapper active big center-align">
                    <div class="spinner-layer spinner-red-only">
                        <div class="circle-clipper left">
                            <div class="circle"></div>
                        </div>
                        <div class="gap-patch">
                            <div class="circle"></div>
                        </div>
                        <div class="circle-clipper right">
                            <div class="circle"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    const request = require('async-request')
    const infiniteScroll = require('vue-infinite-scroll')

    import songCard from '../components/SongCard'

    export default {
        name: 'landingPage',
        components: {
            songCard
        },
        data() {
            return {
                songs: [],
                busy: false
            }
        },
        methods: {
            fetchSongs(from) {
                new Promise(async (resolve, reject) => {
                    this.busy = true
                    this.showLoader()
                    let requestUrl = 'https://chorus.fightthe.pw/api/latest'
                    if (from) requestUrl += '?from=' + from
                    let response = await request(requestUrl)
                    let latestSongs = JSON.parse(response.body).songs
                    this.songs = this.songs.concat(latestSongs)
                    this.busy = false
                    this.hideLoader()
                    resolve()
                })
            },
            showLoader() {
                this.$el.querySelector('.loader').className = this.$el.querySelector('.loader').className.replace(' scale-out', '')
            },
            hideLoader() {
                this.$el.querySelector('.loader').className += ' scale-out'
            },
            async loadMore() {
                await this.fetchSongs(this.songs.length)
            }
        },
        directives: {
            infiniteScroll
        },
        mounted() {
            this.fetchSongs()
        }
    }
</script>

<style scoped>
    .loader {
        margin: 0 calc(50% - 35px);
    }
</style>
