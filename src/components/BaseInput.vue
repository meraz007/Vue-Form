<template>

    <label class="font-semibold leading-none text-gray-300">{{ label }}</label>
    <input type="text" class="leading-none text-gray-50 p-3 focus:outline-none focus:ring  focus:border-blue-700 mt-4 border-0 bg-gray-800 rounded"
    :value="modelValue"
    @input="$emit('update:modelValue',$event.target.value)" />

    <div class="relative">
        <div class="absolute top-1 left-0">
            <p class="text-red-900">{{error}}</p>
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
            type:[String,Number],
            default:''
        },
        error:{
            type:String
        }
    }
}
</script>
