<template>
    <li class="comment-item">
        <div class="d-flex justify-content-between">
            <div class="comment-item__avatar" 
                :style="{ backgroundImage: 'url(' + comment.user.avatar + ')' }">
            </div>
            <button @click="$emit('del-comment', comment.id)" class="btn btn-danger delete-button">x</button>
        </div>
        <h2>{{comment.user.name}}</h2>
        <p>{{comment.content}}</p>
        <div>
            <p>{{comment.createdAt}}</p>
            <div class="mb-3 d-flex justify-content-end align-items-center">
                <button @click="$emit('add-like', comment.id)" class="btn btn-success btn-lg mr-2">
                    Like
                </button> {{comment.likes}} likes
            </div>
        </div>
        <Comments :comments-list="comment.subComments" />
        <AddComment :parent-id="comment.id"/>
    </li>
</template>

<script>
import Comments from './Comments.vue';
import AddComment from './AddComment.vue';

export default {
    components: {
        Comments,
        AddComment
    },
    props: {
        comment: Object
    }
}
</script>

<style>

    .delete-button {
        width: 40px;
        height: 40px;
    }

    .comment-item {
        padding: 15px;
        margin-bottom: 15px;
        border: 1px #ccc solid;
        list-style: none;
    }

    .comment-item__avatar {
        width: 50px;
        height: 50px;
        background-repeat: no-repeat;
        background-position: center;
        background-size: cover;
        border-radius: 50%;
    }

</style>