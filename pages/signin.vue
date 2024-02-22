<script setup lang="ts">
const usersData = await useFetch('http://localhost:3000/user')
// console.log(usersData.data.value, "user data");
const userName = ref("");
type Users = {
    id: string
    email: string
}
if (usersData.data.value) {
    // filteredUser.value = usersData.data.value
}
const email = ref('')
const password = ref('')
// register new user. 
// check if user exist 
// push the user details
async function submit() {
    const getUserData = await useFetch("http://localhost:3000/auth/login", {
        method: "POST",
        body: {
            email: email.value,
            password: password.value
        }
    }
    )
    // refresh user list 
    console.log(getUserData.data.value);

    if (getUserData.data.value) {
        usersData.refresh()
        email.value = ''
        password.value = ''
        navigateTo('/dashboard/products')
    }
}
</script>
<template>
    <div class="h-screen font-[sans poppings]">
        <div class="w-64 h-48 bg-indigo-500 blur-3xl absolute bottom-0 -left-8 rounded-full">
        </div>
        <div class=" w-full justify-center items-center flex flex-col h-full">
            <div class=" border-x-[1px] rounded-xl  border-indigo-500 px-8 py-4">
                <div class=" flex flex-col gap-6">
                    <img src="~/assets/images/KAMBANATION.svg" alt="loading" class=" w-48">
                    <div class="flex flex-col gap-4 ">
                        <p class="text-xl  text-orange-600 ">Sign In</p>
                        <div class="flex flex-col gap-1">
                            <label>Enter Email</label>
                            <input type="email" v-model="email"
                                class=" border-[1px] px-3 border-gray-300 rounded-xl outline-none "
                                placeholder="example@gamil.com">
                        </div>
                        <!-- enter password  -->
                        <div class="flex flex-col gap-2">
                            <label>Enter Password</label>
                            <input type="password" v-model="password"
                                class=" border-[1px] px-3 border-gray-300 rounded-xl outline-none " placeholder="........">
                        </div>
                        <!-- submit login details -->
                        <div class="">
                            <button class=" bg-indigo-500 font-semibold text-sm p-2 rounded-md w-full  text-white"
                                @click="submit()">Login</button>
                        </div>

                        <!-- create a new password  -->
                        <div class="flex w-full justify-between text-xs">
                            <div class="flex gap-1 ">
                                <input type="checkbox" class="">
                                <p>Forgot Password</p>
                            </div>
                            <div class=" text-indigo-500 font-semibold cursor-pointer">
                                <p>Create Account</p>
                            </div>

                        </div>
                        <!-- or signin with google account  -->

                        <div class="flex">
                            <div class=" flex flex-col gap-4 w-full">
                                <p class="text-xl font-semibold text-center">OR</p>
                                <div class=" flex  px-4 py-1 shadow-xl items-center justify-center gap-4 rounded-md w-full">
                                    <img src="~/assets/images/google.svg" alt="loading" class=" w-6">
                                    <p class="text-sm">Sign up with Google</p>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>

            </div>
        </div>
    </div>
</template>
