<script>
// Import BlogPost component and axios here so the default export can reference them
import blogPost from './subcomponents/BlogPost2.vue'
import axios from 'axios'

export default {
    data() {
        return {
            posts: [] // array of post objects
        }
    },
    computed: {
        baseUrl() {
            if (window.location.hostname == 'localhost')
                return 'http://localhost:3000'
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    created() { // created is a hook that executes as soon as Vue instance is created
        axios.get(`${this.baseUrl}/posts`)
        .then(response => {
            // this gets the data, which is an array
            this.posts = response.data
            console.log(response.data)
        })
        .catch(error => {
            this.posts = [{ entry: 'There was an error: ' + error.message }]
        })
    },
    methods: {
        deletePost(id) {
            axios.get(`${this.baseUrl}/deletePost`, {
                params: {
                    id: id
                }
            })  
            .then(response => {
                // Handle successful deletion
                this.posts = this.posts.filter(post => post.id !== id);
            })
            .catch(error => {
                console.error('There was an error deleting the post:', error);
            }); 
        }
    },
    components: {
        blogPost
    }
}
</script>

<template>
    <div>
        <blogPost v-for="post in posts" :key="post.id" :post="post">
            <!-- inject a Delete button into the BlogPost2 slot -->
            <div style="text-align:center; margin-top:10px;">
                <button class="btn btn-primary" @click="deletePost(post.id)">Delete</button>
            </div>
        </blogPost>
    </div>
</template>
