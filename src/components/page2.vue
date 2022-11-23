<template>
  <div class="wrapper">
    <nav class="nav">
      <img src="@/assets/icon-plus.svg" alt="">
      <p>{{ item.score }}</p>
      <img src="@/assets/icon-minus.svg" alt="" class="minus">
    </nav>
    <div class="main">
      <header>
        <div class="user-details">
          <img :src="require('@/assets/' + item.user.image.png)" alt="">
          <p>{{ item.user.username }}</p>
          <p>{{ item.createdAt }}</p>
        </div>
      </header>
      <div class="reply-icon" @click="showRep1">
        <img src="@/assets/icon-reply.svg" alt="">
        <p>Reply</p>
      </div>
      <article>
        {{ item.content }}
      </article>
    </div>
  </div>
  <div class="replies">
    <div class="wrapper reply" v-for="(items, index) in item.replies" :key="index">
      <nav class="nav">
        <img src="@/assets/icon-plus.svg" alt="">
        <p>{{ items.score }}</p>
        <img src="@/assets/icon-minus.svg" alt="" class="minus">
      </nav>
      <div class="main">
        <header>
          <div class="user-details">
            <img :src="require('@/assets/' + items.user.image.png)" alt="">
            <p>{{ items.user.username }}</p>
            <p>{{ items.createdAt }}</p>
          </div>
        </header>
        <div class="reply-icon">
          <img src="@/assets/icon-reply.svg" alt="">
          <p>Reply</p>
        </div>
        <article>
          {{ items.content }}
        </article>
      </div>
    </div>
    <div class="reply-comment" v-if="replycomment">
      <div class="foot">
        <textarea name="" id="" cols="20" rows="3" placeholder="Add a reply" v-model="reply.content"></textarea>

        <button @click="sendReply(item.id)">Reply</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  props: ['item'],
  data() {
    return {
      replycomment: false,
      reply: {
        createdAt: "now",
        score: "0",
        content: "",
        replyingTo: "",
        user:{
          image:{
            png: "image-juliusomo.png",
            webP: "image-juliusomo.webp"
          },
          username: "ola"
        }

      }
    }
  },
  methods: {
    showRep1() {
      this.replycomment = !this.replycomment;
    },
    async sendReply(id) {
      //  this.item.replies.push(this.reply)

       const comments = await axios.get("http://localhost:3000/comments");

      let singleComment = comments.data.filter((item)=> item.id === id )

      console.log(singleComment);
let arr = []
       arr = singleComment.replies
       arr.push(this.reply)

      let newComment = {
                content: singleComment.content,
                createdAt: singleComment.createdAt,
                score: singleComment.score,
                user: singleComment.user,
                replies: arr
            }

      // let arr = []
      // arr.push(this.reply)


      //  const res = await axios.post("http://localhost:3000/comments", {
      //           content: this.comment,
      //           createdAt: "now",
      //           score: 0,
      //           user: {
      //               image: {
      //                   png: "image-juliusomo.png"
      //               },
      //               username: "olawale"
      //           },
      //           replies: arr
      //       });
     
      // const res = await axios.post("http://localhost:3000/comments", {
      //   replies.push(this.reply)

        // replies:[
          
        //   this.reply
        
        // ]
        

        // replies: [
        //   {
        //     createdAt: "now",
        //     score: "0",
        //     content: "",
        //     replyingTo: "",
        //     user: {
        //       image: {
        //         png: "image-juliusomo.png",
        //         webP: "image-juliusomo.webp"
        //       },
        //       username: "ola"
        //     }
        //   }

        // ]
            // })
        
      
    }
  }
}
</script>