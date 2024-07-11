<template>
<!-- Overlay -->
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-40">
        <!-- Modal -->
        <section class="w-full max-w-lg m-auto bg-white rounded-2xl shadow-lg drop-shadow p-4">
            <div class="py-3">
                <div class="border-b-4 border-gray-600 my-2">
                    <h1 class="text-center text-green-700 text-3xl font-bold">Create Model</h1>
                </div>
                <div class="p-2 rounded-lg">
                    <form action="" @submit.prevent="sendDataForm">
                        <inputs-felds idName="usernameId" labelName="Username" typeInput="text" emitsName="emtsUserName" @emtsUserName="emtsUserName"></inputs-felds>
                        <inputs-felds idName="emailId" labelName="Email"  typeInput="email"  emitsName="emtsEmail" @emtsEmail="emtsEmail"></inputs-felds>
                        <inputs-felds idName="phoneId" labelName="Phone"  typeInput="tel"   emitsName="emtsPhone" @emtsPhone="emtsPhone"></inputs-felds>
                        <div class="flex items-center justify-center mt-4">
                            <button type="submit" class="bg-green-500 mx-2 text-white font-bold py-2 px-4 rounded-lg hover:bg-green-600 focus:outline-none focus:shadow-outline">Create</button>
                            <button type="button" @click="showCreateFormModel" class="bg-red-500 mx-2 text-white font-bold py-2 px-4 rounded-lg hover:bg-red-600 focus:outline-none focus:shadow-outline">Exit</button>
                        </div>
                    </form>
                </div>
            </div>
        </section>
    </div>


</template>

<script>
import InputsFelds from "./Input/InputsFelds.vue"

export default {
    name:"CreateModel",
    components: {
        InputsFelds,
    },
    data(){
        return {
            usernameValue:"",
            emailValue:"",
            phoneValue:""
        }
    },
    methods:{
        showCreateFormModel() {
            this.$emit('showCreateFormModel')
        },
        emtsUserName(value) {
            this.usernameValue =value
        },
        emtsEmail(value) {
            this.emailValue =value
        },
        emtsPhone(value) {
            this.phoneValue =value
        },
        sendDataForm(){
            console.log(this.usernameValue);
            let data = {
                id: new Date().toISOString,
                name:this.usernameValue,
                email:this.emailValue,
                phone:this.phoneValue,

            }
            console.log("data:"+data);
            this.$emit("sendDataForm",data)
        }
    },


};
</script>

