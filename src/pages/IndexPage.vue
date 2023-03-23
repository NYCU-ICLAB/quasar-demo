<template>
  <q-page class="flex flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >

    <div>{{ response }}</div>
  </q-page>
</template>

<script>
import { defineComponent, onBeforeMount, ref, reactive } from 'vue'
import { api } from 'boot/axios'

export default defineComponent({
  name: 'IndexPage',
  setup() {
    const item = ref(5)
    let response = ref(null);
    onBeforeMount(()=>{
      api.get("/items/"+ item.value)
        .then((res) => {
          console.log(res.data)
          response.value = res.data.item_id
        })
        .catch((err) => {
          console.log("Error")
          console.log(JSON.stringify(err))
        })
    });

    const test = ref("Hello")

    return {response, test}
  }
})
</script>
