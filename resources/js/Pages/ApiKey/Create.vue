<template>
    <MusicLayout>
        <template #title>
            Create an api key
        </template>
        <template #action>
            <Link :href="route('apikey.index')" class="bg-[#3631a0] text-[#95c4f6] font-bold rounded py-2 px-4">
                Back
            </Link>
        </template>
        <template #content>
            <form @submit.prevent="submit">
                <!-- Titre -->
                <div class="mb-3">
                    <label for="name" class="block text-gray-700 text-lg font-bold mb-2">Name</label>
                    <input id="name" v-model="form.name" type="text"
                           class="bg-[#54569b] text-[#96acd3] shadow rounded-lg py-2 px-4 placeholder-[#5f9cb9] focus:outline-none focus:ring-2 focus:ring-c39977 focus:border-transparent sm:w-96"
                           :class="{ 'border-red-500': form.errors.name }" placeholder="name">
                    <p class="text-red-500 text-xs italic">{{ form.errors.name }}</p>
                </div>
                <br>
                <input type="submit" value="Create" class="bg-[#b665df] text-[#6f4aa0] font-bold rounded py-2 px-4"
                       :class="[form.processing ? 'bg-[#ab409e]' : 'bg-[#bf33de]']" :disabled="form.processing">
            </form>
        </template>
    </MusicLayout>
</template>

<script>
import MusicLayout from '@/Layouts/MusicLayout.vue';
import { Link  } from "@inertiajs/vue3";
export default {
    name: 'Create',
    components: {
        MusicLayout,
        Link,
    },
    data() {
        return {
            form: this.$inertia.form({
                name: '',
                key: '',
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('apikey.store'), {
                //preserveState: false,
            });
        }
    }
}
</script>
