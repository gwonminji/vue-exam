<template>
    <div>
        <h1>props emit</h1>
        <div>Exam2Child이 보낸 메시지 : {{ text }}</div>
        <Exam2Child :keyMsg="msg" @emit1="val => text = val"/>
        <button type="button" @click="changeMsg">click하면 props로 보낼 메시지가 바뀜</button>
        <h1>computed</h1>
        <div>computed : {{ msg2 }}</div>
        <button type="button" @click="changeMsgA">A라고 바꾸기</button>
        <button type="button" @click="changeMsgB">B라고 바꾸기</button>
        <button type="button" @click="changeMsgC">C라고 바꾸기</button>
        <button type="button" @click="changeMsgRemove">지우기</button>
        <h1>child component alert props emit</h1>
        <Alert v-if="isAlert" :alertMsg="alertMsg" @isAlert="val => isAlert = val"/>
        <div>
            <button type="button" @click="openAlert1">alert1</button>
        </div>
        <div>
            <button type="button" @click="openAlert2">alert2</button>
        </div>
        <h1>computed alert</h1>
        <Alert v-if="isAlert "/>
        <button type="button" @click="isAlert = !isAlert">click</button>
    </div>
</template>
<script>
import { ref, watch, computed } from 'vue'
import Exam2Child from '@/components/Exam2Child.vue'
import Alert from '@/components/Alert.vue'

export default {
    components: {
        Exam2Child,
        Alert
    },

    setup() {
        const msg = ref('안녕');
        const msg2 = ref('버튼을 클릭해서 메시지 바꾸기');

        const text = ref('');

        const changeMsg = () => {
            msg.value = 'HI'
        }

        const isAlert = ref(false);

        const alertMsg = ref('');


        watch(
            msg,
            (cur) => {
                msg.value  = cur
            },
            {
                immediate: true
            }
        )

        const changeMsgA = () => {
            msg2.value = "메시지A"
        }

        const changeMsgB = () => {
            msg2.value = "메시지B"
        }

        const changeMsgC = () => {
            msg2.value = "메시지C"
        }

        const changeMsgRemove = () => {
            msg2.value = ""
        }

        const renderMsg2 = computed(() => {
            return msg2;
        })

        const openAlert1 = () => {
            isAlert.value = true;
            alertMsg.value = "alert msg1입니다."
            console.log("isAlert", isAlert.value);
        }

        const openAlert2 = () => {
            isAlert.value = true;
            alertMsg.value = "alert msg2입니다."
            console.log("isAlert", isAlert.value);
        }

        watch(
            isAlert,
            (cur, prev) => {
                console.log("기존 알럿값 ==>", prev);
                console.log("바뀐 알럿값 ==>", cur);
            },
            {
                immediate: true
            }
        )

        return{
            msg,
            changeMsg,
            msg2,
            changeMsgA,
            changeMsgB,
            changeMsgC,
            changeMsgRemove,
            renderMsg2,
            text,
            isAlert,
            openAlert1,
            openAlert2,
            alertMsg
        }
    },
}
</script>