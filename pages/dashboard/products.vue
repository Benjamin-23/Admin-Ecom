<script setup lang="ts">
import { useDropZone } from '@vueuse/core'
const categoriesList = ref(['Hoddies', 'Sweater', 'Shoe', 'T-shirts', 'Design'])
const duration = ref(['Today', 'Weekly', 'Monthly', 'Yearly'])
const selectDuration = ref(0)
const showAddProductUI = ref(false)
const productData = await useFetch('http://localhost:3000/product')

const productName = ref('')
const productCategory = ref('')
const productColor = ref('')
const dropZoneRef = ref<HTMLDivElement>()
const imageName = ref() as Ref<File>
const productPrice = ref("")
const productUnits = ref("")

const { isOverDropZone } = useDropZone(dropZoneRef, (files) => {
    if (files) {
        imageName.value = files[0]
    }
})

async function saveProduct() {
    let formData = new FormData
    formData.append('name', productName.value)
    formData.append('categories', productCategory.value)
    formData.append('color', productColor.value)
    formData.append('price', productPrice.value)
    formData.append('units', productUnits.value)
    formData.append('image', imageName.value)
    if (imageName.value) {
        const data = await useFetch('http://localhost:3000/product', {
            method: 'POST',
            body: formData
        })

    }
    productData.refresh()
    showAddProductUI.value = false

}

</script>

<template>
    <div class="">
        <NuxtLayout name="default">
            <div class=" py-6 px-16 w-full  slotMain">
                <Topheader />
                <div class="mt-8">
                    <div class=" flex flex-col gap-3    ">
                        <p class=" text-2xl font-light">Product</p>
                        <p class="font-light ">Analysis all your products , Upload product details</p>
                        <div class="flex gap-4 font-light text-sm">
                            <p class=" text-indigo-600">Categories:</p>
                            <div class="flex text-gray-400 " v-for=" category in categoriesList">
                                <p>{{ category }}</p>
                            </div>
                            <button class=" text-indigo-500">+ Add</button>
                        </div>
                        <!-- duration  -->
                        <!-- show active time -->
                        <div class="flex justify-between w-[75%]">
                            <div class="" v-for=" (t, index) in duration">
                                <button class=" rounded-xl border-[1px] px-4 py-1 border-[#69666640] text-xs text-[#696666]"
                                    @click="selectDuration = index"
                                    :class="{ 'border-orange-500': selectDuration === index }">{{ t
                                    }} </button>
                            </div>
                            <button class=" bg-indigo-400 px-4 py-1 rounded-xl text-white text-xs"
                                @click=" showAddProductUI = true">Add Product</button>
                        </div>
                        <!-- cards list -->
                        <div class="flex justify-between gap-2 w-[75%]">
                            <!-- card one -->
                            <div
                                class="flex active:border-orange-500 hover:border-orange-500 shadow-md  flex-col border-[1px] border-gray-300 rounded-lg gap-4 px-8 py-4 ">
                                <p class=" text-[#616161] font-semibold">Most Selling Categories</p>
                                <div class="flex flex-col">
                                    <p class="  text-[#696666]">Hoddie 5543</p>
                                    <p class=" text-xs font-light text-[#696666]">(this week)</p>
                                </div>
                            </div>
                            <!-- card two -->
                            <div
                                class="flex flex-col border-[1px] border-gray-300 rounded-xl shadow-md gap-4 px-8 py-4 active:border-orange-500 hover:border-orange-500 ">
                                <p class=" text-[#616161] font-semibold">Most Selling Product</p>
                                <div class="flex flex-col">
                                    <p class="  text-[#696666]">Black Hoddie(Medium)</p>
                                    <p class=" text-xs font-light text-[#696666]">500 this week</p>
                                </div>
                            </div>
                            <!-- card three -->
                            <div
                                class="flex flex-col border-[1px] border-gray-300 rounded-lg gap-4 px-6 py-4 shadow-md  active:border-orange-500 hover:border-orange-500">
                                <p class=" text-[#616161] font-semibold">Total active Products</p>
                                <div class="flex flex-col">
                                    <p class="  text-[#696666] ">Stock 51543</p>
                                    <p class="  text-[#696666]">Value 521,575</p>
                                </div>
                            </div>
                        </div>
                        <div class="">
                            <p>Product List</p>
                            <ProductsList />
                        </div>

                    </div>
                </div>

            </div>
            <!-- upload new product -->
            <Teleport to="body" v-if="showAddProductUI == true">
                <div class="">
                    <OutModal>
                        <div class=" flex flex-col gap-4 shadow-2xl rounded-md bg-white p-4 w-[50%]">
                            <div class="flex justify-between">
                                <p>Product Details</p>
                                <p class=" cursor-pointer" @click="showAddProductUI = false">X</p>
                            </div>

                            <div ref="dropZoneRef"
                                class="flex border-dotted border-[2px] border-gray-400 w-full rounded-md h-32 items-center justify-center">
                                <p class=" text-xl text-gray-300"> {{ imageName ? imageName.name : 'Drop your image Here' }}
                                </p>
                            </div>
                            <div class="flex flex-col gap-4">
                                <div class="flex justify-between">
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Name</label>
                                        <input type="text" class=" outline-none p-1 border-[1px] border-gray-300 rounded-md"
                                            placeholder="Name" v-model="productName">
                                    </div>
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Categories</label>
                                        <input type="text" class=" outline-none border-[1px] border-gray-300 rounded-md p-1"
                                            placeholder="Select categories" v-model="productCategory">
                                    </div>
                                </div>
                                <div class="flex justify-between">
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Price</label>
                                        <input type="text" class=" outline-none p-1 border-[1px] border-gray-300 rounded-md"
                                            placeholder="Ksh 3455" v-model="productPrice">
                                    </div>
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Color</label>
                                        <input type="text" class=" outline-none border-[1px] border-gray-300 rounded-md p-1"
                                            placeholder="Blue" v-model="productColor">
                                    </div>
                                </div>
                                <div class="flex justify-between">
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Code</label>
                                        <input type="text" class=" outline-none p-1 border-[1px] border-gray-300 rounded-md"
                                            placeholder="#23KJK">
                                    </div>
                                    <div class=" flex flex-col gap-2">
                                        <label class=" text-[#616161]">Product Units</label>
                                        <input type="text" class=" outline-none border-[1px] border-gray-300 rounded-md p-1"
                                            placeholder="200 units" v-model="productUnits">
                                    </div>
                                </div>

                            </div>
                            <div class=" rounded-md bg-indigo-500 px-4 py-2  text-white text-center cursor-pointer"
                                @click="saveProduct()">
                                <button>Save Product</button>
                            </div>



                        </div>
                    </OutModal>
                </div>
            </Teleport>
        </NuxtLayout>

    </div>
</template>