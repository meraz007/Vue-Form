<template>
     <div class="w-full flex flex-col mt-8">
        <label class="font-semibold leading-none text-gray-300">{{ label }}</label>
        <p class="text-purple-700 text-opacity-100 mt-2"> {{charCount}}/ {{maxChar}}</p>
        <textarea type="text" 
        class="h-40 text-base leading-none 
        text-gray-50 p-3 focus:outline-none
        focus:border-blue-700 mt-4 
        bg-gray-800 border-0 rounded focus:ring"
        maxlength="5000"
        :value="modelValue"
        @input="$emit('update:modelValue',$event.target.value)"
        >
        </textarea>
        <div class="relative">
            <div class="absolute top-1 left-0">
                <p class="text-red-900">{{error}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
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
        },
    },
     data(){
        return{
        maxChar:5000,
        }
  },
    computed:{
        charCount(){
           return this.modelValue.length
        },
    }
}
</script>
