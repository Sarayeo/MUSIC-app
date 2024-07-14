<template>
    <div class="bg-gradient-to-b from-blue-300 via-blue-400 to-pink-300 py-8 px-4 min-h-screen"> 
        <MusicLayout>
            <template #title>
                <h1 class="text-4xl font-bold text-white mb-6">{{ track.title }}</h1>
            </template>

            <template #action>
                <Link :href="route('tracks.index')"
                      class="bg-pink-600 text-white font-bold rounded py-2 px-4 hover:bg-pink-700 transition duration-300">
                    Back
                </Link>
            </template>

            <template #content>
                <form @submit.prevent="edit" class="max-w-lg mx-auto bg-white p-6 rounded-lg shadow-md">
                    <div class="mb-4">
                        <label for="title" class="block text-gray-700 text-lg font-bold mb-2">Title</label>
                        <input
                            class="bg-blue-500 text-white shadow rounded py-2 px-3 leading-tight focus:outline-none focus:shadow-outline mb-2 w-full"
                            id="title" v-model="form.title" type="text">
                        <p class="text-red-500">{{ form.errors.title }}</p>
                    </div>
                    <div class="mb-4">
                        <label for="artist" class="block text-gray-700 text-lg font-bold mb-2">Artist</label>
                        <input
                            class="bg-blue-500 text-white shadow rounded py-2 px-3 leading-tight focus:outline-none focus:shadow-outline mb-2 w-full"
                            id="artist" name="artist" v-model="form.artist" type="text">
                        <p class="text-red-500">{{ form.errors.artist }}</p>
                    </div>
                    <div class="mb-4">
                        <label for="display" class="block text-gray-700 text-lg font-bold mb-2">Display</label>
                        <select
                            class="w-full bg-blue-500 text-white shadow rounded py-2 px-3 leading-tight focus:outline-none focus:shadow-outline mb-2"
                            name="display" id="display" v-model="form.display">
                            <option :value="true">Oui</option>
                            <option :value="false">Non</option>
                        </select>
                        <p class="text-red-500">{{ form.errors.display }}</p>
                    </div>
                    <input type="submit" value="Modify"
                           class="bg-pink-600 text-white font-bold rounded py-2 px-4 hover:bg-pink-700 transition duration-300 w-full">
                </form>
            </template>
        </MusicLayout>
    </div>
</template>

<script>
import MusicLayout from '@/Layouts/MusicLayout.vue';
import { Link } from '@inertiajs/vue3';

export default {
    name: 'Edit',
    components: {
        MusicLayout,
        Link
    },
    data() {
        return {
            form: this.$inertia.form({
                title: this.track.title,
                artist: this.track.artist,
                display: this.track.display ? true : false,
            })
        }
    },
    props: {
        track: Object,
    },
    methods: {
        edit() {
            console.log('submit');
            this.form.put(route('tracks.update', { track: this.track }));
        }
    }
}
</script>
