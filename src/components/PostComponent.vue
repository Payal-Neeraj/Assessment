<template>
    <div>
        <form @submit="postData" method="post">
        <table style="margin-left: auto;
  margin-right: auto;"><tr><td style="padding-bottom:15px;"><input type="text" name="name" placeholder="Username" v-model="posts.name" > </td>
        <td style="padding-bottom:15px;"><button type="button"  v-clipboard:copy="posts.name" v-clipboard:success="onCopy" v-clipboard:error="onError">Copy!</button></td>
        </tr>
        <tr><td style="padding-bottom:15px;"><input type="email" name="email" placeholder="Email" v-model="posts.email" ></td><td></td>
        </tr>
        <tr><td style="padding-bottom:15px;"><input type="text" name="age" placeholder="Age" v-model="posts.age" ></td><td></td>
        </tr>
        <tr><td><button type="submit" v-on:click="success_msg">Submit</button></td><td></td>
        </tr>
        </table>
            

        </form>
    </div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
import VueClipboard from 'vue-clipboard2'               //it enables to easily copy the content to clipboard
import VueAxios from 'vue-axios'                        //to send POST request
import VueSimpleAlert from 'vue-simple-alert';          //this plugin provides customizable alert popup component

Vue.use(VueSimpleAlert);
Vue.use(VueAxios, axios)
Vue.use(VueClipboard)
    export default {
        name: "PostComponent",
        data(){
            return {
                posts: {
                    name: null,
                    email: null,
                    age: null
                }
            }
        },
        methods:{
            postData(e){
                this.axios.post("http://localhost:8080/api/users",this.posts)   //it sends asynchronous HTTP requests to REST endpoints
                .then((result)=>{
                    console.warn(result)
                })
                e.preventDefault();
            },
            
            onError: function () {
                console.log('Failed to copy texts')
            },
            success_msg: function () {
                this.$alert("Your data is successfully saved in your database")
            }
            
        }
    }

</script>