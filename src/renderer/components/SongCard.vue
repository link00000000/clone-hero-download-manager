<template>
    <div class="col s12 m6 l4 xl3">

        <!-- Card -->
        <div class="card sticky-action hoverable">
            <div class="card-image waves-effect waves-block waves-light">
                <img src="~@/assets/placeholder-album.jpg">
                <img class="activator" :src="directLinks['album.png']" style="position: absolute; height: 100%">
                <i class="material-icons activator tooltipped" data-position="bottom" data-tooltip="Details">more_vert</i>
            </div>
            <div class="card-content">
                <span class="card-title grey-text activator text-darken-4 truncate">{{ name }}</span>
                <p class="truncate activator">{{ artist }}</p>
            </div>
            <div class="card-reveal">
                <span class="card-title grey-text text-darken-4">{{ name }}<i class="material-icons right">close</i></span>
                <p>{{ artist }}</p>
                <p>{{ album }} ({{year}})</p>
                <p>Charted by {{ charter }}</p>
                <p>Uploaded {{ toFuzzyTime(uploadedAt) }}</p>
                <a class="waves-effect waves-light btn-small modal-trigger" :href="'#modal-' + id" style="width: 100%">More</a>
            </div>
            <div class="card-action">
                <a :href="link">DOWNLOAD</a>
            </div>
        </div>

        <song-details-modal
            :id=id
            :name=name
            :artist=artist
            :album=album
            :genre=genre
            :year=year
            :charter=charter
            :length=length
            :diffGuitar=diffGuitar
            :diffBass=diffBass
            :diffRhythm=diffRhythm
            :diffDrums=diffDrums
            :diffKeys=diffKeys
            :diffGuitarghl=diffGuitarghl
            :diffBassghl=diffBassghl
            :isPack=isPack
            :hasForced=hasForced
            :hasOpen=hasOpen
            :hasTap=hasTap
            :hasSections=hasSections
            :hasStarPower=hasStarPower
            :hasSoloSections=hasSoloSections
            :hasVideo=hasVideo
            :hasLyrics=hasLyrics
            :hasNoAudio=hasNoAudio
            :isFolder=isFolder
            :hasBrokenNotes=hasBrokenNotes
            :hasBackground=hasBackground
            :noteCounts=noteCounts
            :lastModified=lastModified
            :uploadedAt=uploadedAt
            :link=link
            :directLinks=directLinks
            :sources=sources
            :hashes=hashes
        />

    </div>
</template>

<script>
    import songDetailsModal from './SongDetailsModal'

    export default {
        name: 'songCard',
        props: [
            "id",
            "name",
            "artist",
            "album",
            "genre",
            "year",
            "charter",
            "length",
            "diffGuitar",
            "diffBass",
            "diffRhythm",
            "diffDrums",
            "diffKeys",
            "diffGuitarghl",
            "diffBassghl",
            "isPack",
            "hasForced",
            "hasOpen",
            "hasTap",
            "hasSections",
            "hasStarPower",
            "hasSoloSections",
            "hasVideo",
            "hasLyrics",
            "hasNoAudio",
            "isFolder",
            "hasBrokenNotes",
            "hasBackground",
            "noteCounts",
            "lastModified",
            "uploadedAt",
            "link",
            "directLinks",
            "sources",
            "hashes",
        ],
        components: {
            songDetailsModal
        },
        methods: {
            toMMSS(duration) {
                let sec_num = duration
                let minutes = Math.floor(sec_num / 60)
                let seconds = sec_num - (minutes * 60)

                if (minutes < 10) minutes = "0" + minutes
                if (seconds < 10) seconds = "0" + seconds

                return minutes + ':' + seconds
            },
            toFuzzyTime(time) {
                return moment(time).fromNow()
            }
        },
        mounted() {
            M.Tooltip.init(this.$el.querySelector('.tooltipped'))
        },
    }
</script>

<style>
    .card-title i {
        position: absolute;
        right: 10px;
        top: 10px;
    }
    .card-content > * {
        cursor: pointer;
    }
    .card-image > .material-icons {
        position: absolute;
        right: 5px;
        bottom: 10px;
        color: white;
        text-shadow: 1px 1px 1px black
    }
    .modal-content .album {
        position: absolute;
        right: 0;
        top: 0;
        height: 100%;
        -webkit-mask-image: linear-gradient(90deg, transparent, black);
        position: fixed;
    }
</style>
