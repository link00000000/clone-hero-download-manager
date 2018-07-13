<template>
    <!--
        TODO:
            Add audio preview to modal usb FABs
     -->
    <div :id="'modal-' + id" class="modal modal-fixed-footer">
        <div class="modal-content">
            <h4>{{ name }}</h4>
            <h6>{{ artist }} - {{ album }} ({{ year }})</h6>
            <img v-if="directLinks['album.png']" class="responsive-img album hide-on-small-only" :src="directLinks['album.png']">
            <img v-else class="responsive-img album hide-on-small-only" src="~@/assets/placeholder-album.jpg">
            <audio v-if="directLinks['song.ogg']"><source  :src="directLinks['song.ogg']" type="audio/ogg"></audio>
            <div class="fixed-action-btn">
                <a class="btn-floating btn-large red">
                    <i class="large material-icons">mode_edit</i>
                </a>
                <ul>
                    <li><a class="btn-floating red"><i class="material-icons">insert_chart</i></a></li>
                    <li><a class="btn-floating yellow darken-1"><i class="material-icons">format_quote</i></a></li>
                    <li><a class="btn-floating green"><i class="material-icons">publish</i></a></li>
                    <li><a class="btn-floating blue"><i class="material-icons">attach_file</i></a></li>
                </ul>
                </div>
            <div class="col xl5">
                <table>
                    <tbody>
                        <tr><td>Name</td><td>{{ name || 'N/A' }}</td></tr>
                        <tr><td>Album</td><td>{{ album || 'N/A' }}</td></tr>
                        <tr><td>Artist</td><td>{{ artist || 'N/A' }}</td></tr>
                        <tr><td>Genre</td><td>{{ genre || 'N/A' }}</td></tr>
                        <tr><td>Release Year</td><td>{{ year || 'N/A' }}</td></tr>
                        <tr><td>Charter</td><td>{{ charter || 'N/A' }}</td></tr>
                        <tr><td>Duration</td><td>{{ toMMSS(length) || 'N/A' }}</td></tr>
                        <tr><td>Guitar Difficulty</td><td>{{ diffGuitar || 'N/A' }}</td></tr>
                        <tr><td>Bass Difficulty</td><td>{{ diffBass || 'N/A' }}</td></tr>
                        <tr><td>Rhythm Difficulty</td><td>{{ diffRhythm || 'N/A' }}</td></tr>
                        <tr><td>Drums Difficulty</td><td>{{ diffDrums || 'N/A' }}</td></tr>
                        <tr><td>Keys Difficulty</td><td>{{ diffKeys || 'N/A' }}</td></tr>
                        <tr><td>GHL Guitar Difficulty</td><td>{{ diffGuitarghl || 'N/A' }}</td></tr>
                        <tr><td>GHL Bass Difficulty</td><td>{{ diffBassghl || 'N/A' }}</td></tr>
                        <tr><td>Has Forced Notes</td><td>{{ hasForced ? 'true' : 'false' }}</td></tr>
                        <!-- Removed due to an empty object being returned -->
                        <!-- <tr><td>Has Open Notes</td><td>{{ hasOpen }}</td></tr> -->
                        <tr><td>Has Tap Notes</td><td>{{ hasTap ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Sections</td><td>{{ hasForced ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Star Power</td><td>{{ hasStarPower ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Solo Sections</td><td>{{ hasSoloSections ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Video Background</td><td>{{ hasVideo ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Lyrics</td><td>{{ hasLyrics ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Audio</td><td>{{ !hasNoAudio ? 'true' : 'false' }}</td></tr>
                        <tr><td>Is Folder</td><td>{{ isFolder ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Broken Notes</td><td>{{ hasBrokenNotes ? 'true' : 'false' }}</td></tr>
                        <tr><td>Has Background Image</td><td>{{ hasBackground ? 'true' : 'false' }}</td></tr>
                        <!-- <tr><td>Note Count</td><td>{{ noteCounts }}</td></tr> -->
                        <tr><td>Last Modified</td><td>{{ lastModified ? toFuzzyTime(lastModified) + ' (' + formatTimestamp(lastModified) + ')' : 'N/A' }}</td></tr>
                        <tr><td>Uploaded</td><td>{{ uploadedAt ? formatTimestamp(uploadedAt) : 'N/A' }}</td></tr>
                    </tbody>
                </table>
            </div>
        </div>
        <div class="modal-footer">
            <a href="#!" class="modal-close waves-effect waves-orange btn-flat orange-text">DOWNLOAD</a>
            <a href="#!" class="modal-close waves-effect waves-green btn-flat">CLOSE</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'songDetailsModal',
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
            },
            formatTimestamp(time) {
                return moment(time).format('MMMM Do YYYY [at] h:mm:ss A')
            }
        },
        mounted() {
            M.Modal.init(this.$el)
            M.FloatingActionButton.init(this.$el.querySelector('.fixed-action-btn'))
        }
    }
</script>

<style scoped>
    .fixed-action-btn {
        bottom: 45px;
    }
</style>
