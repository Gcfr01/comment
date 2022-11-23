<template>
  <div class="container">
    <div v-for="(item, index) in comments" :key="index">
      <Page2 :item="item"  />
    </div>
    <div class="public">
      <div class="foot">
        <textarea name='' id="" cols="33" rows="5" placeholder="Add a comments" v-model="comment"></textarea>
        <div>
          <button @click="sendComment">SEND</button>
        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Page2 from './page2.vue';
export default {
    name: "HelloWorld",
    components: { 
      Page2 
    },
    data() {
        return {
            comment: "",
            comments: [],
            // replies:[]
        };
    },
    methods: {
       
        async sendComment() {
            // var today = new Date();
            // var time = today.getHours();
            const res = await axios.post("http://localhost:3000/comments", {
                content: this.comment,
                createdAt: "now",
                score: 0,
                user: {
                    image: {
                        png: "image-juliusomo.png"
                    },
                    username: "olawale"
                },
                replies: []
            });
            this.comment = "";
            this.$router.go();
            log;
        }
    },
    async created() {
        const res = await axios.get("http://localhost:3000/comments"); 
        this.comments = res.data;
        console.log(res.data);
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="@/components/style.css" >

</style>
