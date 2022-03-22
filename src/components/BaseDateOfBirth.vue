<template>
   <div class="md:flex items-center mt-12">
        <div class="w-full md:w-1/2 flex flex-col">
        <label class="font-semibold leading-none text-gray-300">Date Of Birth</label>
            <div class="relative">
                <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                    <svg class="w-5 h-5 mt-4 text-gray-50 dark:text-gray-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd"></path></svg>
                </div>
                <input datepicker datepicker-format="yyyy/mm/dd" type="text" class="leading-none bg-gray-800 border-0 text-gray-50 focus:ring  focus:border-blue-700 sm:text-sm rounded focus:outline-none focus:border-blue-700 block w-full pl-10 p-3 mt-4" placeholder="Select date"
                :value="modelValue"
                @input="$emit('update:modelValue',$event.target.value)" />
                
            </div>
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
            type:[String],
            default:''
        },
        error:{
            type:String
        }
    }
}
</script>

