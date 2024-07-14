<template>
    <div>
        <nav class="bg-gradient-to-r from-blue-300 to-pink-300 shadow-lg rounded-lg">
            <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
                <div class="relative flex h-16 items-center justify-between">
                    <div class="flex-1 flex justify-center">
                        <div class="hidden sm:ml-6 sm:block">
                            <div class="flex space-x-4">
                                <Link v-if="$page.props.auth.user" :href="route('tracks.index')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-blue-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('tracks') ? 'bg-blue-700' : 'bg-blue-500']">
                                    My Tracks
                                </Link>
                                <Link v-if="$page.props.auth.user" :href="route('playlists.index')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-pink-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('playlists') ? 'bg-pink-700' : 'bg-pink-500']">
                                    My Playlists
                                </Link>
                                <Link v-if="$page.props.auth.user" :href="route('apikey.index')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-purple-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('apikey') ? 'bg-purple-700' : 'bg-purple-500']">
                                    My API Keys
                                </Link>
                                <Link v-if="!$page.props.auth.user" :href="route('login')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-blue-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('login') ? 'bg-blue-700' : 'bg-blue-500']">
                                    Log In
                                </Link>
                                <Link v-if="!$page.props.auth.user" :href="route('register')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-pink-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('register') ? 'bg-pink-700' : 'bg-pink-500']">
                                    Register
                                </Link>
                                <Link v-if="$page.props.auth.user" as="button" method="POST" :href="route('logout')"
                                      class="text-white font-bold rounded py-2 px-4 hover:bg-red-700 hover:text-white transition duration-300"
                                      :class="[route().current().includes('logout') ? 'bg-red-700' : 'bg-red-500']">
                                    Logout
                                </Link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </nav>
        <div class="px-8 py-6">
            <div class="flex justify-between items-center">
                <h4 class="text-3xl font-bold text-gray-800">
                    <slot name="title"/>
                </h4>
                <div>
                    <slot name="action"/>
                </div>
            </div>

            <div class="mt-4">
                <slot name="content"/>
            </div>
        </div>
    </div>
</template>

<script>
import { Link } from "@inertiajs/vue3";

export default {
    name: 'MusicLayout',
    components: {
        Link
    }
}
</script>
