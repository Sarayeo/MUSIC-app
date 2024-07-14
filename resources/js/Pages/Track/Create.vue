<template>
    <div class="bg-gradient-to-b from-blue-300 via-blue-400 to-pink-300 py-8 px-4 min-h-screen">
        <MusicLayout>
            <template #title>
                <h1 class="text-4xl font-bold text-white mb-6">Create a Music</h1>
            </template>
            <template #action>
                <Link :href="route('tracks.index')"
                      class="bg-pink-600 text-white font-bold rounded py-2 px-4 hover:bg-pink-700 transition duration-300">
                    Back
                </Link>
            </template>
            <template #content>
                <form @submit.prevent="submit" class="py-8 px-4 rounded bg-white shadow-md max-w-lg mx-auto">
                    <!-- Title -->
                    <div class="mb-4">
                        <label for="title" class="block text-gray-700 text-lg font-bold mb-2">Title</label>
                        <input id="title" v-model="form.title" type="text"
                               class="bg-blue-500 shadow rounded py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline w-full"
                               :class="{ 'border-red-500': form.errors.title }" placeholder="Title">
                        <p class="text-red-500 text-xs italic">{{ form.errors.title }}</p>
                    </div>

                    <!-- Artist -->
                    <div class="mb-4">
                        <label for="artist" class="block text-gray-700 text-lg font-bold mb-2">Artist</label>
                        <input id="artist" v-model="form.artist" type="text"
                               class="bg-blue-500 shadow rounded py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline w-full"
                               :class="{ 'border-red-500': form.errors.artist }" placeholder="Artist">
                        <p class="text-red-500 text-xs italic">{{ form.errors.artist }}</p>
                    </div>

                    <!-- Display -->
                    <div class="mb-4">
                        <label for="display" class="block text-gray-700 text-lg font-bold mb-2">Display</label>
                        <select name="display" id="display" v-model="form.display"
                                class="bg-blue-500 shadow rounded py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline w-full"
                                :class="{ 'border-red-500': form.errors.display }">
                            <option :value="true">Oui</option>
                            <option :value="false">Non</option>
                        </select>
                        <p class="text-red-500 text-xs italic">{{ form.errors.display }}</p>
                    </div>

                    <!-- Image -->
                    <div class="mb-4">
                        <label for="image" class="block text-gray-700 text-lg font-bold mb-2">Image</label>
                        <input @input="form.image = $event.target.files[0]" type="file" name="image" id="image"
                               class="w-full text-gray-700">
                        <p class="text-red-500 text-xs italic">{{ form.errors.image }}</p>
                    </div>

                    <!-- Audio -->
                    <div class="mb-4">
                        <label for="audio" class="block text-gray-700 text-lg font-bold mb-2">Audio</label>
                        <input @input="form.music = $event.target.files[0]" type="file" name="audio" id="audio"
                               class="w-full text-gray-700">
                        <p class="text-red-500 text-xs italic">{{ form.errors.audio }}</p>
                    </div>

                    <input type="submit" value="Create"
                           class="bg-pink-600 text-white font-bold rounded py-2 px-4 hover:bg-pink-700 transition duration-300 w-full"
                           :class="[form.processing ? 'bg-pink-400' : 'bg-pink-600']" :disabled="form.processing">
                </form>
            </template>
        </MusicLayout>
    </div>
</template>

<script>
import MusicLayout from '@/Layouts/MusicLayout.vue';
import { Link } from "@inertiajs/vue3";

export default {
    name: 'Create',
    components: {
        MusicLayout,
        Link,
    },
    data() {
        return {
            form: this.$inertia.form({
                title: '',
                artist: '',
                display: true,
                image: null,
                music: null,
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('tracks.store'), {
                //preserveState: false,
            });
        }
    }
}
</script>

<style>
body {
    background-color: #3e3bea;
}

#artist {
    background-color: #e350eb;
    color: #cf95f6;
}
</style>
