<template>
  <div class="container">
    <div id="app">
      <Header />
      <Comments :comments-list="commentsList" 
                @del-comment="delComment"
                @add-like="addLike"/>
      <AddComment @create-comment="addComment"/>
    </div>
  </div>
</template>

<script>

  import Comments from './components/Comments.vue';
  import Header from './components/Header.vue';
  import AddComment from './components/AddComment.vue';

  export default {
    name: 'app',
    components: {
      Comments,
      AddComment,
      Header
    },
    data() {
      return {
        commentsList: [
          {
            id: 1,
            user: {
              id: 1,
              name: 'Ilon Musk',
              avatar: 'https://static.mk.ru/upload/entities/2019/10/18/22/articles/detailPicture/1e/29/a3/a5/a0b656599fde72d6d31da7415a8cbad4.jpg'
            },
            content: 'Hello, I\'m Ilon Musk',
            createdAt: 'Sun Nov 24 2019 17:52:13 GMT+0200',
            likes: 798,
            subComments: [{
              id: 1,
              user: {
                id: 1,
                name: 'Ilon Musk',
                avatar: 'https://static.mk.ru/upload/entities/2019/10/18/22/articles/detailPicture/1e/29/a3/a5/a0b656599fde72d6d31da7415a8cbad4.jpg'
              },
              content: 'Hello, I\'m Ilon Musk',
              createdAt: 'Sun Nov 24 2019 17:52:13 GMT+0200',
              likes: 798,
            }]  
          },
          {
            id: 2,
            user: {
              id: 2,
              name: 'Bill Gates',
              avatar: 'https://upload.wikimedia.org/wikipedia/commons/9/91/Bill_Gates_1977.png'
            },
            content: 'Hello, I\'m Bill Gates',
            createdAt: 'Sun Nov 24 2019 17:52:13 GMT+0200',
            likes: 9798,
            subComments: [{
              id: 1,
              user: {
                id: 1,
                name: 'Ilon Musk',
                avatar: 'https://static.mk.ru/upload/entities/2019/10/18/22/articles/detailPicture/1e/29/a3/a5/a0b656599fde72d6d31da7415a8cbad4.jpg'
              },
              content: 'Hello, I\'m Ilon Musk',
              createdAt: 'Sun Nov 24 2019 17:52:13 GMT+0200',
              likes: 798,
            }]   
          }
        ],
      }
    },
    methods: {
      addComment(payload) {
        if(payload.parentId) {
          this.commentsList.map((i)=>{
            if(i.id == payload.parentId) {
              payload.commentData.id = i.subComments.length + 1;
              i.subComments.push(payload.commentData);
            } 
          });
        } else {
          payload.commentData.id = this.commentsList.length + 1;
          this.commentsList.push(payload.commentData);
        }
      },
      delComment(id){
        this.commentsList = this.commentsList.filter(commentsList => commentsList.id !== id);
      },
      addLike(id) {
        this.commentsList.map((i)=>{
          if(id == i.id) {
            i.likes++;
          }
        });
      }
    }
  }

</script>

<style>

  /* Box sizing rules */
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }

  /* Remove default padding */
  ul[class],
  ol[class] {
    padding: 0;
  }

  /* Set core body defaults */
  body {
    min-height: 100vh;
    scroll-behavior: smooth;
    text-rendering: optimizeSpeed;
    line-height: 1.5;
  }

  /* Remove list styles on ul, ol elements with a class attribute */
  ul[class],
  ol[class] {
    list-style: none;
  }

  /* A elements that don't have a class get default styles */
  a:not([class]) {
    text-decoration-skip-ink: auto;
  }

  /* Make images easier to work with */
  img {
    max-width: 100%;
    display: block;
  }

  /* Natural flow and rhythm in articles by default */
  article > * + * {
    margin-top: 1em;
  }

  /* Inherit fonts for inputs and buttons */
  input,
  button,
  textarea,
  select {
    font: inherit;
  }

  /* Remove all animations and transitions for people that prefer not to see them */
  @media (prefers-reduced-motion: reduce) {
    * {
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.01ms !important;
      scroll-behavior: auto !important;
    }
  }

</style>
