<template>
    <div class="w-96 mx-auto">
        <div>
            <div>
                <input v-model="title" class="mb-3 p-2 w-96 rounded-3xl border border-slate-300 " type="text" placeholder="title">
            </div>
            <div>
                <textarea v-model="content" class="mb-3 p-2 w-96 rounded-3xl border border-slate-300 " placeholder="content"></textarea>
            </div>
            <div class="flex">
                <div>
                    <input @change="storeImage" ref="file" type="file" class="hidden">
                    <a href="#" class="mb-3  block p-2 w-32 rounded-3xl bg-sky-500 text-white text-center hover:bg-red-600" @click.prevent="selectFile()">Image</a>
                </div>
                <div>
                    <a v-if="image" @click.prevent="image=null" class="ml-12 mb-3 block p-2 w-32 rounded-3xl bg-sky-500 text-white text-center" href="#">Cancel</a>
                </div>
            </div>
            <div v-if="image">
                <img :src="image.url" alt="preview">
            </div>
            <a @click.prevent="store" href="#" class="ml-auto block p-2 w-32 rounded-3xl bg-green-600 text-white text-center hover:bg-red-600">Publish</a>
        </div>
    </div>
</template>

<script>

export default {
    name: "Personal",
    data(){
        return {
            title: '',
            content: '',
            image: null,
        }
    },
    methods: {
        store(){
            const id = this.image ? this.image.id : null ;
          axios.post('/api/posts',{title: this.title, content: this.content, image_id: id})
              .then(res => {
                  console.log(res);
              });
        },
        selectFile() {
            this.fileInput = this.$refs.file;
            this.fileInput.click();
        },
        storeImage(e) {
            let file = e.target.files[0]
            const formData = new FormData()
            formData.append('image', file)
            axios.post('/api/post_images', formData, {
                headers: {
                    'Content-Type': 'multipart/form-data'
                }
            })
                .then(res => {
                    this.image = res.data.data
                })
        },
    }
}
</script>

<style scoped>

</style>
