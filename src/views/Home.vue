<template>
  <div class="home">
    {{UserInfo}}
    <div class="w-full bg-gray-800 h-screen">
    <div class="bg-gradient-to-b from-blue-800 to-blue-600 h-96"></div>
    <div class="max-w-5xl mx-auto px-6 sm:px-6 lg:px-8 mb-12">
        <div class="bg-gray-900 w-full shadow rounded p-8 sm:p-12 -mt-72">
            <p class="text-3xl font-bold leading-7 text-center text-white">Contact me</p>
            <form action="" method="post">
                <div class="md:flex items-center mt-12">
                    <div class="w-full md:w-1/2 flex flex-col">
                      <BaseInput v-model="UserInfo.name"
                        label="Name"
                        type="text"/>
                    </div>
                    <div class="w-full md:w-1/2 flex flex-col md:ml-6 md:mt-0 mt-4">
                      <BaseInput v-model="UserInfo.email"
                        label="Email"
                        type="email"/>
                    </div>
                </div>
                  <BaseDateOfBirth 
                    v-model="UserInfo.dateOfBirth"
                    label="Date Of Birth"
                    type="text"/>
                    <BaseTextArea 
                      v-model="UserInfo.bio"
                      label="Bio"
                      type="text"/>
                  <BasePhoto
                  v-model="UserInfo.photo"
                      label="Photo"
                      type="file"/>
                    
                <div class="flex items-center justify-center w-full">
                    <button class="mt-9 font-semibold leading-none text-white py-4 px-10 bg-blue-700 rounded hover:bg-blue-600 focus:ring-2 focus:ring-offset-2 focus:ring-blue-700 focus:outline-none">
                        Send message
                    </button>
                </div>
            </form>
        </div>
    </div>
</div>
  </div>
</template>

<script>
import BaseInput from '../components/BaseInput.vue'
import BaseTextArea from '../components/BaseTextArea.vue'
import BasePhoto from '../components/BasePhoto.vue'
import BaseDateOfBirth from '../components/BaseDateOfBirth.vue'

export default {
  name: "Home",

  components:{
    BaseInput,
    BaseTextArea,
    BasePhoto,
    BaseDateOfBirth
  },

  data(){
    return{
      UserInfo:{
        name:"",
        email:"",
        dateOfBirth:"",
        bio:"",
        photo:null
      }
    }
  }
  }
</script>
