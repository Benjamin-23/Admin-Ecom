<template>
    <!-- <NuxtPage /> -->
    <div class="flex w-screen">
        <div class="flex h-screen bg-orange-100 w-[20%] py-8 justify-center">
            <div class="flex flex-col justify-between">
                <!-- logo  -->
                <div class="flex flex-col gap-8">
                    <div class="">
                        <img src="~/assets/images/KAMBANATION.svg" alt="loading" class="w-44" />
                    </div>
                    <div class="flex flex-col gap-4">
                        <div class="flex gap-4">
                            <img src="~/assets/images/dashboard.svg" alt="loading" class="w-4" />
                            <NuxtLink to="/dashboard" class="text-lg">Dashboard</NuxtLink>
                        </div>
                        <div class="flex gap-4">
                            <img src="~/assets/images/product.svg" alt="loading" class="w-4" />
                            <NuxtLink to="/dashboard/products" class="text-[#7B09A6] text-lg">Products</NuxtLink>
                        </div>
                        <div class="flex gap-4">
                            <img src="~/assets/images/orders.svg" alt="loading" class="w-4" />
                            <NuxtLink to="/dashboard" class="text-lg">Orders</NuxtLink>
                        </div>
                        <div class="flex gap-4">
                            <img src="~/assets/images/reports.svg" alt="loading" class="w-4" />
                            <NuxtLink to="/dashboard" class="text-lg">Reports</NuxtLink>
                        </div>
                        <div class="flex gap-4">
                            <img src="~/assets/images/setting.svg" alt="loading" class="w-4" />
                            <NuxtLink to="/dashboard" class="text-lg">Settings</NuxtLink>
                        </div>
                    </div>
                </div>

                <div class=" flex items-center rounded-md px-4 py-2 bg-gray-200 justify-center gap-2 "
                    @click="navigateTo('/signin')">
                    <img src="~/assets/images/logout.svg" alt="" class="w-3" />
                    <button>Logout</button>
                </div>
            </div>
        </div>

        <slot class="w-[80%] "></slot>
    </div>
</template>
