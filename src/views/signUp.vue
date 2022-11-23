<template>
    <div class="container">
           <h1>Sign-Up Here</h1>  
            <div class="sign-form">
                <form action="">
                    <label for="name">FullName</label>
                    <input type="text" name="" id="" v-model="name">
                    <label for="username">Username</label>
                    <input type="text" name="" id="" v-model="username">
                    <label for="username">Password</label>
                    <input type="text" name="" id="" v-model="password">
                    <button>Create Account</button>
               </form>
            </div>           
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name:"",
                username:"",
                password:""
            }
        },
        methods: {
           async signUp(){
                const res = await axios.post("http://localhost:3000/currentUser", {
                    username: this.username,
                    name: this.name,
                    password: this.ZU
            })
        },
      }
    }
</script>

<style lang="css" scoped>
    .container{
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    h1{
        margin-bottom: 20px;
    }
    label, input{
        display: block;
        height: 30px;
        width: 100%;
    }
    input{
        margin-bottom: 10px;
    }
    button{
        padding: 10px 20px;
    }
    .sign-form{
        border: 1px solid grey;
        padding: 20px 50px;
    }
</style>