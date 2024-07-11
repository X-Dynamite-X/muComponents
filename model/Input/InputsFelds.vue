<template>
    <div class="mb-4 flex items-center">
        <label :for="idName"   class="w-1/3 text-gray-700 font-bold">{{labelName}}</label>
        <input :type="typeInput" @input="emitDynamicEvent" :value="inputValue.default" v-model="inputValue.default" :id="idName" class="w-2/3 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" :placeholder="`Enter your ${labelName}`">
    </div>

</template>

<script>
export default {
    name:"InputsFelds",
    data(){
        return{
            inputValue:{
                type: String,
                default: '',
                require:true,
            },
        }
    },
    methods: {
        emitDynamicEvent(event) {
            this.$emit(this.emitsName, event.target.value);
        }
    },
    computed:{
        chackDatainput(){
            console.log(this.inputValue);
            console.log(this.emtsName);
            console.log(11);
            if(this.inputValue.length > 0){
                console.log("chackDatainput is run ");
                return this.inputValue
            }   else{
                return ""
            }
        }
    },
    
    props:{
        labelName:{
            type:String,
            required:true
        },
        idName:{
            type:String,
            required:true
        },
        typeInput:{
            type:String,
            required:true,
            default(){
                return "text"
            }
        },
        emitsName:{
            type:String,
        },
    

},

}
</script>

<style>

</style>