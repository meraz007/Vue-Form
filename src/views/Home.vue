<template>
  <div class="home">
    <div class="w-full bg-gray-800 h-screen">
    <div class="bg-gradient-to-b from-blue-800 to-blue-600 h-96"></div>
    <div class="max-w-5xl mx-auto px-6 sm:px-6 lg:px-8 mb-12">
        <div class="bg-gray-900 w-full shadow rounded p-8 sm:p-12 -mt-72">
            <p class="text-3xl font-bold leading-7 text-center text-white">User Info</p>
            <form @submit.prevent="formSubmit" method="post">
                <div class="md:flex items-center mt-12">
                  <div
                  @drop="onDrop"
                  @dragenter.prevent
                  @dragover.prevent
                  >
                  
                  </div>
                    <div class="w-full md:w-1/2 flex flex-col" @dragstart="startDrag" id="123"
                    draggable="true">
                      <BaseInput 
                      v-model="name"
                        label="Name"
                        type="text"
                        :error="nameError"
                        />
                    </div>
                    <div class="w-full md:w-1/2 flex flex-col md:ml-6 md:mt-0 mt-4" @dragstart="startDrag" id="123"
                    draggable="true">
                      <BaseInput 
                      v-model="email"
                        label="Email"
                        type="email"
                        :error="emailError"/>
                    </div>
                </div>
                <div draggable="true">
                  <BaseDateOfBirth 
                    v-model="dateOfBirth"
                    label="Date Of Birth"
                    type="text"
                    :error="dateOfBirthError"
                    />
                </div>
                    <div draggable="true">
                      <BaseTextArea 
                      v-model="bio"
                      label="Bio"
                      type="text"
                      :error="bioError"
                      :maxChar="maxChar"
                      />
                    </div>
                    <div draggable="true">
                      <BasePhoto
                      v-model="photo"
                      label="Photo"
                      type="file"
                      :error="photoError"
                      />
                    </div>
                    <div draggable="true">
                      <SubmitButton />
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
import SubmitButton from '../components/SubmitButton.vue'

import { useField } from 'vee-validate'
export default {
  name: "Home",

  components:{
    BaseInput,
    BaseTextArea,
    BasePhoto,
    BaseDateOfBirth,
    SubmitButton,
  },

  setup(){
    
    const startDrag =(event)=>{
      event.dataTransfer.dropEffect ='move'
      event.dataTransfer.effectAllowed ='move'
      event.dataTransfer.setData('inputField',event.target.id)
    }
    const onDrop=(event)=>{
      const item =event.dataTransfer.getData('inputField')
      event.target.appendChild(document.getElementById(item));
    }
   /*
    const onDragging = (ev) => {
        console.log(ev);
        ev.dataTransfer.setData("text", ev.target.id);
    };
    const allowDrop = (ev) => {
        ev.preventDefault();
    };
    const drag = (ev) => {
        ev.dataTransfer.setData("text", ev.target.id);
    };
    const drop = (ev) => {
        ev.preventDefault();
        let data = ev.dataTransfer.getData("text");
        console.log(data);
        ev.target.appendChild(document.getElementById(data));
    }
*/
    //FOR NAME
    const name =useField('name',function(value){
       if(!value) return 'This field is required'
       const nameRegex = /^[a-zA-Z\s.]*$/;
       if(!nameRegex.test(value)){
         return "only alphabet, dot and space is allowed"
       }
       return true
    })
    //FOR EMAIL
    const email =useField('email',function(value){
      if(!value) return 'This field is required'

      const emailRegex = RegExp(
        /^[a-zA-Z0-9.]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/);
      if(!emailRegex.test(String(value).toLowerCase())){
        return 'Please Enter a valid email address'
      }
      return true
        })
    
    //FOR DATE OF BIRTH
    const dateOfBirth=useField('dateOfBirth',function(value){
      if(!value) return 'This field is required'
      //validation for leap
      if(value % 400 ===0){
        return true
      }else{
        return false
      }
    })
    //FOR BIO
    const bio =useField('bio',function(value){
       if(!value){
         return 'This field is required'
       } 
       else{
         return true
       }
    })
    //FOR photo
    const photo =useField('photo',function(value){
       if(!value){
         return 'This field is required'
       } 
       else{
         return true
       }
    })
    function formSubmit(){
      alert('Submitted')
    }
        return {
          //startDrag,
          formSubmit,
          name:name.value,
          email:email.value,
          emailError:email.errorMessage,
          nameError:name.errorMessage,
          dateOfBirth:dateOfBirth.value,
          dateOfBirthError:dateOfBirth.errorMessage,
          bio:bio.value,
          bioError:bio.errorMessage,
          photo:photo.value,
          photoError:photo.errorMessage,
          startDrag,
          onDrop
        }
  },

  }
</script>

