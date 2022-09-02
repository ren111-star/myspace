<template>
<div class="row">
    <div class="col-4 img-field">
        <img class="img-fluid" :src="user.photo" alt="">
    </div>
    <div class="col-8">
        <div class="username">{{ user.username }}</div>
        <div class="fans">粉丝数: {{user.followerCount}}</div>
        <button v-if="!user.is_followed" @click="follow" type="button" class="btn btn-secondary btn-sm">+关注</button>
        <button v-else type="button" @click="unfollow" class="btn btn-secondary btn-sm">已关注</button>
    </div>
</div>
</template>

<script>

export default {
    name: "UserProfileInfo",
    props: {
        user: {
            type: Object,
            required: true
        },
    },
    setup(context) {
        const follow = () => {
            context.emit('follow');
        };

        const unfollow = () => {
            context.emit('unfollow');
        }

        return {
            follow,
            unfollow
        }
    }

}
</script>

<style scoped>
img {
    border-radius: 50%;
}
.username{
    font-weight: bold;
}
.fans {
    font-size: 12px;
    color: grey;
}
button {
    padding: 2px 4px;
    font-size: 12px;
}
.img-field {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>