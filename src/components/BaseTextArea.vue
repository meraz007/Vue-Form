<template>
     <div class="w-full flex flex-col mt-8">
        <label class="font-semibold leading-none text-gray-300">{{ label }}</label>
        <textarea type="text" 
        class="h-40 text-base leading-none 
        text-gray-50 p-3 focus:outline-none
        focus:border-blue-700 mt-4 
        bg-gray-800 border-0 rounded"
        :value="modelValue"
        @input="$emit('update:modelValue',$event.target.value)"
        >
        </textarea>
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
        }
    }
}
</script>