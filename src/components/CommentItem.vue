<template>
    <li class="comment-item">
        <div class="d-flex justify-content-between">
            <div class="comment-item__avatar" 
                :style="{ backgroundImage: 'url(' + comment.user.avatar + ')' }">
            </div>
            <button @click="$emit('del-comment', comment.id)" class="btn btn-danger">x</button>
        </div>
        <h2>{{comment.user.name}}</h2>
        <p>{{comment.content}}</p>
        <div class="d-flex justify-content-between">
            {{comment.createdAt}}
            <div>
                <button @click="$emit('add-like', comment.id)" class="btn btn-success">
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