<template>
    <div class="w-full flex flex-col mt-8">
        <label class="font-semibold leading-none text-gray-300">Upload Photo</label>
        <input class="leading-none 
        text-gray-50 p-3 focus:outline-none 
        focus:border-blue-700 mt-4 border-0 
        bg-gray-800 rounded focus:ring " 
        aria-describedby="user_avatar_help" 
        accept="image/x-png,image/jpg,image/jpeg"
        ref="myFile"
        @change="selectedFile"
        id="user_avatar" 
        type="file"
        :value="modelValue"
        @input="$emit('update:modelValue',$event.target.value)"
        >
        <div class="mt-1 text-sm text-gray-500 dark:text-gray-300" id="user_avatar_help">PNG, JPG, jpeg up to 5MB and 600x600</div>
    </div>
    <div class="relative">
    <div class="absolute top-1 left-0">
        <p class="text-red-900">{{error}}</p>
    </div>
</div>

<div v-if="preview" class="preview">
    <img class="object-cover h-48 w-96" :src="preview">
    <p class="text-gray-300">Size:{{image.size/1024}}KB</p>
</div>
<div class="relative">
    <div class="absolute top-1 left-0">
        <p v-if="imageError" class="text-red-900"> {{imageError}}</p>
    </div>
</div>
</template>

<script>
export default {
    data(){
        return{
            image:{
                size:"",
                width:"",
                height:"",
            },
            imageError:'',
            preview: null,
            image1: null,
        }
    },
     props:{
        label:{
            type:String,
            default:''
        },
        modelValue:{
            type:String,
            default:''
        },
        error:{
            type:String
        }
    },
    methods:{
    selectedFile(event) {
      this.imageError = '';
      const MAX_SIZE = 5000000;
      const MAX_WIDTH = 600;
      const MAX_HEIGHT = 600;
      
      let file = this.$refs.myFile.files[0];

      //MAX_SIZE
      if(!file || file.type.indexOf('image/') !== 0) return;
      this.image.size = file.size;
      if(this.image.size > MAX_SIZE) {
        this.imageError = `The image size (${this.image.size}) is too much (max is ${MAX_SIZE}).`;
        return;
      }
      
      let reader = new FileReader();
      
      reader.readAsDataURL(file);
      reader.onload = evt => {
        let img = new Image();
        img.onload = () => {
          this.image.width = img.width;
          this.image.height = img.height;
          console.log(this.image);
          //MAX_WIDTH
          if(this.image.width > MAX_WIDTH) {
            this.imageError = `The image width (${this.image.width}) is too much (max is ${MAX_WIDTH}).`;
            return;
          }
          else{
            //preview image
            var input = event.target;
            if (input.files) {
                reader.onload = (e) => {
                this.preview = e.target.result;
                }
                this.image1=input.files[0];
                reader.readAsDataURL(input.files[0]);
            }
          }
          //MAX_HEIGHT
          if(this.image.height > MAX_HEIGHT) {
            this.imageError = `The image height (${this.image.height}) is too much (max is ${MAX_HEIGHT}).`;
            return;
          }
          
          
        }
        img.src = evt.target.result;
      }

      reader.onerror = evt => {
        console.error(evt);
      }
    
      
    },
  }
}
</script>
<style scoped>

</style>