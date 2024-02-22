<script setup lang="ts">
import { useDropZone } from '@vueuse/core'
interface Product {
    name: string
    categories: string
    color: string
    image: string
}
const productList = ref([]) as Ref<any[]>
const productData = await useFetch('http://localhost:3000/product', {
    method: "GET"
})
const imageTrun = (str: any, len: any) => str.length > len ? str.slice(0, len) + '...' : str
// const { base64: fileImage } = useBase64(imageName);

// function onDrop(files: File[] | null) {
//     if (files) {
//         imageName.value = files[0]
//         console.log(imageName.value, "picha yangu");
//     }
// }



async function removeAll() {
    const removeAllProducts = useFetch('http://localhost:3000/product/removeAll', {
        method: "DELETE"
    })
    productData.refresh()
}

watchEffect(() => {
    productData.data.value
})


</script>
<template>
    <div class="flex flex-col gap-4">
        <table class=" table-auto w-[75%]">
            <thead class=" text-gray-600 border-b-[1px] border-gray-400">
                <tr>
                    <th>No</th>
                    <th>Product Name</th>
                    <th>Product Image</th>
                    <th>Product Price</th>
                    <th>Categories</th>
                    <th>Units</th>
                    <th></th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr class=" border-b-[1px] text-gray-400 text-sm" v-for="( prod, index) in productData.data.value"
                    :key="index">
                    <td>{{ index + 1 }}</td>
                    <td>{{ prod.name }}</td>
                    <td class="">{{ imageTrun(prod.image, 12) }}
                    </td>
                    <td class=" text-center">{{ prod.price }}</td>
                    <td>{{ prod.categories }}</td>
                    <td>{{ prod.units }}</td>
                    <td></td>
                    <td></td>

                </tr>
                <!-- <tr class=" border-b-[1px] text-gray-400 text-sm">
                    <td>2</td>
                    <td>White Hoddies</td>
                    <td class="">whiteHoddies.svg</td>
                    <td class=" text-center">4000</td>
                    <td>Hoddies</td>
                    <td>12</td>
                    <td></td>
                    <td></td>

                </tr>
                <tr class=" border-b-[1px] text-gray-400 text-sm">
                    <td>3</td>
                    <td>White Hoddies</td>
                    <td class="">whiteHoddies.svg</td>
                    <td class=" text-center">4000</td>
                    <td>Hoddies</td>
                    <td>12</td>
                    <td></td>
                    <td></td>

                </tr>
                <tr class=" border-b-[1px] text-gray-400 text-sm">
                    <td>4</td>
                    <td>White Hoddies</td>
                    <td class="">whiteHoddies.svg</td>
                    <td class=" text-center">4000</td>
                    <td>Hoddies</td>
                    <td>12</td>
                    <td></td>
                    <td></td>

                </tr>
                <tr class=" border-b-[1px] text-gray-400 text-sm">
                    <td>5</td>
                    <td>White Hoddies</td>
                    <td class="">whiteHoddies.svg</td>
                    <td class=" text-center">4000</td>
                    <td>Hoddies</td>
                    <td>12</td>
                    <td></td>
                    <td></td> -->

                <!-- </tr> -->
            </tbody>
        </table>
        <!-- footer -->

        <div class="flex gap-4 items-center">
            <div class=" border-[1px] border-gray-300 rounded-md px-4 py-2 text-sm">
                <p class=" text-[#2D2C2C]">5</p>
            </div>
            <div class=" bg-gray-200 rounded-md px-4 py-2 text-sm">
                <p class=" text-[#2D2C2C]">Next</p>
            </div>
            <p class=" text-[#2D2C2C]">1</p>
            <div class=" bg-gray-200 rounded-md px-4 py-2 text-sm">
                <p class=" text-[#2D2C2C]">Previous</p>
            </div>

        </div>
    </div>
</template>
<style>
th,
td {
    padding: 5px 25px 5px 0;
}
</style>
