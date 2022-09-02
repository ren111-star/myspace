<template>
    <ContentBase>
      <div class="row">
        <div class="col-3">
          <div class="card">
            <div class="card-body">
              <UserProfileInfo :user="user" @follow="follow" @unfollow="unfollow"/>
            </div>
          </div>
          <UserProfileWriter @post_a_post="post_a_post"/>
        </div>
        <div class="col-9">
          <UserProfilePosts :posts="posts"/>
        </div>
      </div>
    </ContentBase>
  </template>
  
  <script>
  // @ is an alias to /src
  import ContentBase from '../components/ContentBase.vue'
  import UserProfileInfo from '@/components/UserProfileInfo.vue';
  import UserProfilePosts from '../components/UserProfilePosts.vue';
  import UserProfileWriter from '../components/UserProfileWriter.vue'
  import { reactive } from 'vue'
  import { useRoute } from 'vue-router';
  import $ from 'jquery'
  import { useStore } from 'vuex';
    
  export default {
    name: 'UserProfileView',
    components: {
      ContentBase,
      UserProfileInfo,
      UserProfilePosts,
      UserProfileWriter
    },
    setup() {
      const route = useRoute();
      const userId = route.params.userId;
      const store = useStore();

      const user = reactive({
      });

      const posts = reactive({
      });

      $.ajax({
        url: "https://app165.acapp.acwing.com.cn/myspace/getinfo/",
        type: "get",
        data: {
          user_id: userId
        },
        headers: {
          'Authorization' : "Bearer " + store.state.user.access,
        },
        success(resp) {
          console.log(resp);
          user.id = resp.id;
          user.username = resp.username;
          user.photo = resp.photo;
          user.followerCount = resp.followerCount;
          user.is_followed = resp.is_followed;
        }
      })

      const follow = () => {
        if (user.is_followed) return;
        user.is_followed = true;
        user.followCount ++;
      };

      const unfollow = () => {
        if (!user.is_followed) return;
        user.is_followed = false;
        user.followCount --;
      };

      const post_a_post = (content) =>{
        posts.count++,
        posts.posts.unshift({
          id: posts.count,
          userId: 1,
          content: content,
        })
      }

      return {
        user,
        follow,
        unfollow,
        posts,
        post_a_post
      }
    }
  }
  </script>
  
  <style scoped>
  
  </style>