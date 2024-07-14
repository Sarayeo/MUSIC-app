<template>
    <div class="bg-gradient-to-b from-blue-300 via-blue-400 to-pink-300 py-8 px-4 min-h-screen"> 
        <MusicLayout>
            <template #title>
                <h1 class="text-4xl font-bold text-white mb-6">My Tracks</h1>
            </template>

            <template #action>
                <Link v-if="$page.props.isAdmin" :href="route('tracks.create')" class="bg-pink-600 text-white font-bold rounded py-2 px-4 hover:bg-pink-700 transition duration-300">
                    Add a Music
                </Link>
            </template>

            <template #content>
                <div>
                    <div class="flex flex-col sm:flex-row justify-center align-center gap-4 sm:gap-20 mb-6">
                        <h3 class="text-lg text-white">Search a Song</h3>
                        <div class="flex items-center gap-2">
                            <input v-model='filter' placeholder="Title" type="search" class="bg-blue-500 text-white shadow rounded-lg py-2 px-4 placeholder-white focus:outline-none focus:ring-2 focus:ring-blue-300 focus:border-transparent sm:w-96">
                            <button type="submit" class="flex items-center justify-center bg-blue-500 text-white rounded-lg p-2 hover:bg-blue-600 transition duration-300">
                                <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 15l5-5m0 0l-5-5m5 5H4"></path>
                                </svg>
                            </button>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                        <Tracks v-for="track in filterTrack" :key="track.id" :track="track" @played="play(track)"/>
                    </div>
                </div>
            </template>
        </MusicLayout>
    </div>
</template>

<script>
import { Link } from "@inertiajs/vue3";
import MusicLayout from "@/Layouts/MusicLayout.vue";
import Tracks from "@/Components/Track/Track.vue";

export default {
    name: 'Index',
    components: {
        MusicLayout,
        Tracks,
        Link,
    },
    data() {
        return {
            audio: null,
            currentTrack: null,
            filter: ''
        }
    },
    props: {
        tracks: Array,
    },
    computed: {
        filterTrack() {
            return this.tracks.filter(track =>
                track.title.toLowerCase().includes(this.filter.toLowerCase()) ||
                track.artist.toLowerCase().includes(this.filter.toLowerCase())
            );
        }
    },
    methods: {
        play(track) {
            const url = 'storage/' + track.music;

            if (!this.currentTrack) {
                this.audio = new Audio(url);
                this.audio.play();
            } else if (this.currentTrack !== track.uuid) {
                this.audio.pause();
                this.audio.src = url;
                this.audio.play();
            } else {
                this.audio.paused ? this.audio.play() : this.audio.pause();
            }

            this.currentTrack = track.uuid;
            this.audio.addEventListener('ended', () => this.currentTrack = null);
        },
    }
}
</script>
