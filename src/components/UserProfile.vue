<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">
        @{{user.username}}

      </h1>
       <div class="user-profile__admin-badge" v-if="user.isAdmin">
            Admin
        </div>
       <div class="user-profile__admin-badge" v-else>
            Not Admin
        </div>

      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{followers}}
      </div>
        <form class="user-profile__create-twoot">
            <label for="newTwoot">
                <strong>New Twoot :</strong>
            </label>
            <textarea name="" id="newTwoot"  rows="4"></textarea>

            <div class="user-profile__create-twoot-type">
                <label for="newTwootType">Type:</label>
                <select name="" id="newTwootType">
                    <option value="" v-for="(option,index) in twootTypes" :key="index">

                    </option>
                </select>
            </div>

        </form>
    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem v-for="twoot in user.twoots" v-bind:key="twoot.id" :username="user.username" :twoot="twoot" @favourite="toggleFavorite"/>
    </div>
  </div>
</template>

<script>

import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components:{TwootItem},
  data(){
    return {
        twootTypes:{
            {value:'draft', name:'Draft'},
            {value:'instant', name :'Instant twoot'}
        },
        followers: 0,
        user:{
        id: 1,
        username:'_MitchellRomney',
        firstName :'Mitchell',
        lastName : 'Romney',
        email:'test@testuser.com',
        isAdmin : false,
        twoots:[
            {id: 1, content: 'twooter is Amazing'},
            {id: 2, content:"Don't forget to subscribe to the earth flat club"}
        ]
      }
    }
  },
  watch:{
    followers(newFollowersCount, oldFollowersCount){
      if( oldFollowersCount < newFollowersCount ){
        console.log(`User ${this.user.username} gained a follower`);
      }
    }
  },
  computed:{
    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods:{
    followUser(){
      this.followers++;
    },
    toggleFavorite(id){
        console.log(`Favorited twoot ${id}`);
    }
  },
  mounted(){
    this.followUser();
  }
}
</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding : 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge{
    background-color: rebeccapurple;
    color: white;
    border-radius: 5px;   
    margin-right: auto;
    padding: 0px 10px;
    width: fit-content;
}

.user-profile__create-twoot{
    border-top: 1px solid #DFE3E8;
    display: flex;
    flex-direction: column;
    padding-top: 20px;
}

</style>
