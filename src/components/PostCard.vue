<template>
    <div class="container">
        <b-card class="card">
            <b-card-title class="title">{{post.title}}</b-card-title>
            <b-card-text>{{post.body}}</b-card-text>
            <b-card-text class="author">{{post.author.name}}</b-card-text>
        </b-card>
    </div>
</template>

<script>
export default {
    name: "PostCard",
    props: {
        post: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped lang="scss">
.container {
    padding: 0;
    max-width: 420px;
    width: 100%;
    .card {
        display: inline-block;
        margin-bottom: 16px;
        .title {
            color: dodgerblue;
        }
        .author {
            color: grey;
        }
    }
}
</style>