<template>
    <q-page class="flex flex-center full container">
      <div class="full child container">
        <div class="q-pa-none example-column-row-wrapping full child container">
          <div class="row full child">
            <div class="col-12 col-md-9 q-pa-none full child container">
              <NodeCard></NodeCard>
            </div>
          </div>
        </div>
      </div>
      
    </q-page>
  </template>
  
  <script>
  import { defineComponent } from 'vue'
  import NodeCard from 'src/components/NodeCard.vue'
  
  export default defineComponent({
    components: { NodeCard },
    name: 'NodePage'
  })
  </script>
  