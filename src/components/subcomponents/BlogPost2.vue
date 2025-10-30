<script>
export default {
    // Accept a `post` object with id, subject, entry, mood
    props: {
        post: {
            type: Object,
            required: true
        }
    },
    computed: {
        imgLoc() {
            const mood = (this.post.mood || '').toLowerCase();
            return `/assets/${mood}.png`;
        }
    }
}
</script>


<template>
    <!-- Bootstrap card that displays the post and exposes a slot for actions -->
    <div class="card" style="width: 18rem;">
        <img :src="imgLoc" class="card-img-top" alt="">
        <div class="card-body">
            <h5 class="card-title">Blog {{ post.id }} Subject {{ post.subject }}</h5>
            <p class="card-text">{{ post.entry }}</p>
            <!-- Slot where parent can inject buttons (e.g. Delete) -->
            <slot></slot>
        </div>
    </div>

</template>

