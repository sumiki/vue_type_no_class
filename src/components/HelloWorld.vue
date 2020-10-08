<script lang="ts">
import { defineComponent, SetupContext, ref, reactive, Ref, computed } from 'vue';
type Props = {
    msg: string;
};

export default defineComponent({
    props: {
        msg: {
            type: String,
            default: "default Value"
        }
    },
    setup(props: Props, context: SetupContext) {
        console.log(props);
        console.log(context);
        const customMessage: Ref<string> = ref('abc')
        const messages: Ref<string[]> = ref([]);
        const state = reactive({
            content1: 'content1',
            content2: 'content2',
            count: 0,

        })

        function addMessage() {
            console.log(customMessage);
            messages.value.push(customMessage.value);
        }

        function handleSwitch( e: Event ){
            e.preventDefault()
            state.count = state.count + 1;
            const c1 = state.content1;
            const c2 = state.content2;
            state.content1 = c2;
            state.content2 = c1;
        }

        const counter = computed(() => `${ state.count } times`)

        return {
            customMessage,
            messages,
            state,
            addMessage,
            handleSwitch,
            counter
        }
    }
});
</script>

<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <div>
            <input type="text" v-model="customMessage"><input type="submit" text="Add" @click="addMessage">
            <div>{{customMessage}}</div>
            <hr>
            <div v-for="(message, index) in messages" v-bind:key="index">{{message}}</div>
            <hr>
            <h5>Reactive</h5>
            <div>{{ counter }}</div>
            <div><a href="#" @click="handleSwitch" >{{ state.content1 }}</a></div>
            <div>{{ state.content2 }}</div>
        </div>
    </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
