<template>
    <div>
        <ul class="comments-list">
            <CommentItem 
                :comment="comment" 
                :key="comment.id" 
                @del-comment="$emit('del-comment', comment.id)"
                @add-like="$emit('add-like', comment.id)"
                v-for="comment in commentsList"/>
        </ul>
    </div>
</template>
<script>
import CommentItem from './CommentItem';

export default {
    name: 'Comments',
    components: {
        CommentItem
    },
    props: {
        commentsList: Array
    }
}
</script>
<style>
    .comments-list {
        padding: 0;
        margin-top: 15px;
    }
</style>