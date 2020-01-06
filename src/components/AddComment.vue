<template>
    <form @submit.prevent="submitComment">
        <textarea class="form-control mt-1" v-model="commentText"/>
        <button class="mt-3 btn btn-primary" type="submit">
            Add Comment
        </button>
    </form>
</template>

<script>

export default {
    props:{
        parentId: Number
    },
    data() {
        return {
            commentText: ''
        }
    },
    methods: {
        submitComment() {
            const commentData = {
                user: {
                    id: 1,
                    name: 'Ilon Musk',
                    avatar: 'https://images11.esquire.ru/upload/img_cache/f01/f01c00158714d664cdffdd7c2d0f2682_ce_1999x1247x0x98_cropped_960x600.jpg'
                },
                content: this.commentText,
                createdAt: new Date(),
                likes: 0  
            }
            // eslint-disable-next-line
            console.warn(commentData);
            this.$emit('create-comment',{ parentId: this.parentId, commentData });
            this.commentText = '';
        }
    }
}

</script>