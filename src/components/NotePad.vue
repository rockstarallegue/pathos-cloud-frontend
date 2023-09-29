<template>
    <div class="full fit light-2-glass rounded-2 q-pa-sm" style="min-height: 32em; min-width: 40em;">
      <div class="full-width q-pa-xs grey-square light-1-glass rounded-2">
        <span class="nasalization text-blue-grey q-px-xs"><q-icon name="edit_note"></q-icon> Create note</span>
        <div class="q-pa-xs full-width row">
          <!-- ADD NOTE -->
          <div class="col-6 q-pa-none" style="min-height: 10em">
              <div class="text-blue-grey text-left nasalization font-8 q-pa-none bg-grey-12 rounded-2">
                <div class="full-width bg-blue-grey text-grey-12 rounded-2 q-pa-xs grey-borders">
                  <div class="full-width row q-pa-xs">
                    <div class="col-8 font-12 text-bold q-pt-xs q-px-xs">
                      Write something
                    </div>
                    <div class="col-4 text-right q-px-xs">
                      <q-btn dense flat icon="cloud_upload" 
                        class="bg-blue-grey text-white q-pa-none q-px-xs font-11"/>
                    </div>
                  </div>
                  <div class="bg-grey-12 q-pa-none rounded-2">
                    <q-input
                      v-model="text"
                      filled
                      type="textarea"
                      color="blue-grey"
                      class="full-width rounded-2 font-8 q-pa-xs"
                      style="min-height: 7em"
                  />
                  </div>
                  
                </div>
              </div>
          </div>
          <!-- ADD FILE -->
          <div class="col-6 q-pa-none q-pl-sm" style="min-height: 9em">
              <div class="text-blue-grey full-width text-left nasalization font-8 q-pa-none rounded-2">
                <div class="full-width bg-blue-grey rounded-2 q-pa-xs" style="min-height: 14.5em">
                  <q-uploader
                      url="http://localhost:4444/upload"
                      label="Upload file"
                      color="blue-grey"
                      flat
                      class="full-width text-blue-grey bg-grey-12"
                  />
                </div>
              </div>
          </div>
        </div>
      </div>
      
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  // import NoteBox from 'src/components/Builders/Boxes/NoteBox.vue'
  
  export default defineComponent({
    // components: { NoteBox },
    name: 'NotePad'
  })
  </script>
  