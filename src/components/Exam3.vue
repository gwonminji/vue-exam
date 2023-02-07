<template>
    <div>
        <Exam3Child>
            <!-- <button>버튼</button> -->
            <template v-slot:left>
                <button>왼쪽 버튼</button>
            </template>
            <template v-slot:right>
                <button>오른쪽 버튼</button>
            </template>
        </Exam3Child>
        <Exam3Child>
            <!-- <button>버튼</button> -->
            <template v-slot:right>
                <button>오른쪽 버튼</button>
            </template>
            <template v-slot:center>
                <p>텍스트11</p>
            </template>
        </Exam3Child>
        <Exam3Child>
            <template v-slot:center>
                <p>텍스트1</p>
            </template>
        </Exam3Child>
        <Exam3Child>
            <template v-slot:center>
                <p>텍스트2</p>
            </template>
        </Exam3Child>
        <div class="copy-form">
            <p ref='copyText'>가나다라마바</p>
            <button type="button" @click="copy">copy</button>
        </div>
        <input type="text" ref='copyInput'>
    </div>
</template>
<script>
import { ref } from 'vue'
import Exam3Child from '@/components/Exam3Child.vue'
export default {
    components: {
        Exam3Child
    },
    setup() {
        const copyText = ref(null);
        const copyInput = ref(null);
        const copy = () =>{
            //value.innerText로 엘리먼트 텍스트값 추출
            // alert(copyText.value.innerText);
            navigator.clipboard.writeText(copyText.value.innerText).then(() => {
                alert("복사가 완료되었습니다.");
                copyInput.value.focus();
            })
        }
        return{
            copyText,
            copyInput,
            copy
        }
    },
}
</script>
<style>
.copy-form{
    display: flex;
}
</style>