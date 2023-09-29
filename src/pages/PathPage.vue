<template>
  <q-page class="flex flex-center full container">
    <div class="full child container">
      <div class="q-pa-none example-column-row-wrapping full child container">
        <div class="row full child">
          <div class="col-12 col-md-9 q-pa-none full child container">
            <PathCard @pin="(pin) => $emit('pin', pin)"></PathCard>
          </div>
        </div>
      </div>
    </div>
    
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import PathCard from 'src/components/PathCard.vue'

export default defineComponent({
  components: { PathCard },
  name: 'IndexPage'
})
</script>
