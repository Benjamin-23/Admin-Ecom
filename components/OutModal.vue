<template>
    <div class=" absolute top-0 right-0 w-[83.65%] bg-[#D9D9D965] h-screen flex justify-center items-center"
        @click="$emit('close')">
        <slot></slot>
    </div>
</template>