<template>
    <div>
        <!-- <slot></slot> -->
        <slot name="right"></slot>
        <slot name="left"></slot>
        <slot name="right"></slot>
        <slot name="center"></slot>
    </div>
</template>
<script>
export default {
    setup() {
        return{

        }
    },
}
</script>