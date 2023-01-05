<template>
    <div class="flex justify-between p-8 w-96 mx-auto text-center text-sm">
        <div>
            Subscribers
            <div>
                {{stats.subscribers_count}}
            </div>
        </div>
        <div>
            Likes
            <div>
                {{stats.likes_count}}
            </div>
        </div>
        <div>
            Posts
            <div>
                {{stats.posts_count}}
            </div>
        </div>
        <div>
            Follows
            <div>
                {{stats.followings_count}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Stat",

    props: [
        'stats'
    ]
}
</script>

<style scoped>

</style>
