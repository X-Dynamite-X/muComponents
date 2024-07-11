<template>
  <!-- Overlay -->
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-40">
        <!-- Modal -->
        <section class="w-full max-w-lg m-auto bg-white rounded-2xl shadow-lg drop-shadow p-4">
            <div class="py-3">
                <div class="border-b-4 border-gray-600 my-2">
                    <h1 class="text-center text-orange-600 text-3xl font-bold">Edit Model</h1>
                </div>
                <div class="p-2 rounded-lg">
                    <form action="">
                        <div class="mb-4 flex items-center">
                            <label for="username"   class="w-1/3 text-gray-700 font-bold">User Name</label>
                            <input type="text" :value="frend.name"   id="username" class="w-2/3 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" placeholder="Enter your username">
                        </div>
                        <div class="mb-4 flex items-center">
                            <label for="email" class="w-1/3 text-gray-700 font-bold">Email</label>
                            <input type="email" id="email" class="w-2/3 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" placeholder="Enter your email">
                        </div>
                        <div class="mb-4 flex items-center">
                            <label for="password" class="w-1/3 text-gray-700 font-bold">Password</label>
                            <input type="password" id="password" class="w-2/3 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" placeholder="Enter your password">
                        </div>
                        <div class="mb-4 flex items-center">
                            <label for="confirm-password" class="w-1/3 text-gray-700 font-bold">Confirm Password</label>
                            <input type="password" id="confirm-password" class="w-2/3 px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" placeholder="Confirm your password">
                        </div>
                        <div class="flex items-center justify-center mt-4">
                            <button type="button" class="bg-orange-500 mx-2 text-white font-bold py-2 px-4 rounded-lg hover:bg-orange-600 focus:outline-none focus:shadow-outline">Edit</button>
                            <button type="button" @click="showEditFormModel" class="bg-red-500 mx-2 text-white font-bold py-2 px-4 rounded-lg hover:bg-red-600 focus:outline-none focus:shadow-outline">Exit</button>
                        </div>
                    </form>
                </div>
            </div>
        </section>
    </div>


</template>

<script>
export default {
    name:"EditModel",
    methods:{
        showEditFormModel() {
            this.$emit('showEditFormModel')
        },
    },
    
    props:{
        frend:{
            type:Object,
            default:()=>({}),
        },
    },
 
};
</script>

