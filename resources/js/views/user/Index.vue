<template>
    <div class="w-96 mx-auto">
        <div v-if="users">
            <div class="flex justify-between items-center mb-4 pb-6 border-b border-gray-200" v-for="user in users">
                <router-link :to="{name: 'user.show',params: {id: user.id}}">
                    <p>{{ user.id }}</p>
                    <p>{{ user.name }}</p>
                    <p>{{ user.email }}</p>
                </router-link>
                <div>
                    <a @click.prevent="toggleFollowing(user)"
                       :class=" ['mb-3  block p-2 w-32 rounded-3xl',user.is_followed ? 'bg-white text-sky-500 border border-sky-500 text-center' : 'bg-sky-500 text-white text-center hover:bg-red-600']" href="#">
                    {{user.is_followed ? 'Unfollowed' : 'Follow'}}</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Index",

    data() {
        return {
            users: []
        }
    },
    mounted() {
        this.getUsers()
    },

    methods: {
        getUsers() {
            axios.get('/api/users/')
                .then(res => {
                    this.users = res.data.data
                })
        },
        toggleFollowing(user){
            axios.get(`/api/users/${user.id}/toggle_following`)
                .then(res => {

                     user.is_followed = res.data.is_followed
                })
        }
    }
}
</script>

<style scoped>

</style>
