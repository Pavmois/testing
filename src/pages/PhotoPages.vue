<template>
    <v-container>
        <photoForm v-if="photos.length < 11" @addPhoto="addPhoto"/>
        <div v-else>Вы не можете</div>
        <v-row>
            <photo
            v-bind:key = "photo.id"
            v-for="photo in photos"
            v-bind:photo='photo'
            @openPhoto="openPhoto"
            />
        </v-row>
        <photoDialog :photo="currentPhoto" v-model="dialogVisible"/>
    </v-container>
</template>

<script>
import photo from "@/components/photo/photo"
import photoForm from "@/components/photo/photoForm.vue";
import photoDialog from "@/components/photo/photoDialog.vue";
export default {
    components: {
        photo,photoForm,photoDialog
    },
    data: () => ({
        photos: [],
        currentPhoto: {},
        dialogVisible: false
    }),
    mounted() {
        this.fetchTodo();
    },
    methods: {
        fetchTodo() {
            this.axios.get('https://jsonplaceholder.typicode.com/photos?_limit=10')
            .then(response => this.photos = response.data)
        },
        addPhoto(photo) {
            this.photos.push(photo)
        },
        openPhoto(photo) {
            this.currentPhoto = photo;
            this.dialogVisible = true;
        }
    }
}
</script>

<style scoped>

</style>