<template>
    <div class="w-full flex flex-col mt-8">
        <label class="font-semibold leading-none text-gray-300">Upload Photo</label>
        <input class="leading-none 
        text-gray-50 p-3 focus:outline-none 
        focus:border-blue-700 mt-4 border-0 
        bg-gray-800 rounded focus:ring " 
        aria-describedby="user_avatar_help" 
        id="user_avatar" 
        type="file"
        :value="modelValue"
        @input="$emit('update:modelValue',$event.target.value)"
        >
        <div class="mt-1 text-sm text-gray-500 dark:text-gray-300" id="user_avatar_help">PNG, JPG, jpeg up to 5MB and 600x600</div>
        <div class="preview">
            <img v-if="modelValue" class="object-cover h-48 w-96" :src="modelValue">
        </div>
    </div>
    <p class="text-red-900">{{error}}</p>
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
        }
    },
}
</script>