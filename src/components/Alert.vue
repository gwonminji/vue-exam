<template>
    <div class="alert">
        <div class="alert__dimmed"></div>
        <div class="alert__content">
            <p class="alert__msg">{{ alertMsg }}</p>
            <button type="button" class="alert__close" @click="hideAlert">확인</button>
        </div>
    </div>
</template>
<script>
import { ref } from 'vue'

export default {
    props: {
        alertMsg: {
            type: String
        }
    },
    emits: ["isAlert"],
    setup(props, context) {
        const isAlert = ref(false);

        const { emit } = context;

        const hideAlert = () => {
            isAlert.value = false
            emit('isAlert', isAlert.value);
        }
        return{
            isAlert,
            hideAlert
        }
    },
}
</script>
<style>
.alert{
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
    z-index: 9998;
}
.alert__dimmed{
    position: fixed;
    width: 100vw;
    height: 100vh;
    background: rgba(0 , 0, 0, 0.3);
}
.alert__content{
    position: relative;
    width: 300px;
    padding: 20px;
    background: #fff;
    border-radius: 8px;
    z-index: 9999;
}
.alert__msg{
    margin: 0;
}
.alert__close{
    position: absolute;
    right: 20px;
    bottom: 20px;
}
/* .alert::before{
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    z-index: 9998;
}
.alert{
    position: relative;
    width: 300px;
    padding: 20px;
    background: #fff;
    border-radius: 8px;
    z-index: 9999;
}
.alert__close{

} */
</style>