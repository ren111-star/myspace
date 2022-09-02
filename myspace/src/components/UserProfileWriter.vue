<template>
    <div class="card edit-field">
        <div class="card-body">
            <!-- <label for="edit-post" class="form-label"></label> -->
            <textarea v-model="content" class="form-control" placeholder="写点什么~" id="edit-post" rows="7"></textarea>
            <button  @click="post_a_post" type="button" class="btn btn-primary btn-sm">发帖</button>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    name: "UserProfileWriter",
    setup(props, context) {
        let content = ref('');

        const post_a_post = () => {
            context.emit("post_a_post", content.value);
            content.value = "";
        };

        return {
            content,
            post_a_post,
        };
    }
}
</script>

<style scoped>
.edit-field{
    margin-top: 10px;
}
button {
    margin-top: 10px;
}
</style>