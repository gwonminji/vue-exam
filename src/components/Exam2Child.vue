<template>
    <div>
        {{ keyMsg }}
        <button type="button" @click="emitSend">부모에게 메시지 보내기</button>
    </div>
</template>
<script>
import { ref } from 'vue'

export default {
    props: {
        keyMsg: {
            type: String
        }
    },
    emits: ['emit1'],
    setup(props, context) {
        let emit1 = ref('');

        const { emit } = context;

        const emitSend = () => {
            emit1.value = 'text 보내기';
            emit('emit1', emit1.value);
        }
        return{
            emitSend
        }
    },
}
</script>