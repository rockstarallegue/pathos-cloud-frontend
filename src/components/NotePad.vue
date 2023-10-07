<template>
    <div class="full child bg-gral rounded-2 q-pa-sm" style="max-height: 40em; max-width: 50em;">
      <div class="full-width q-pa-none q-pb-sm">
        <div class="q-py-xs full-width row">
          <!-- ADD NOTE -->
          <div class="col-6 q-pa-none" style="min-height: 10em">
              <div class="text-blue-grey text-left nasalization font-8 q-pa-none bg-grey-12 rounded-2">
                <div class="full-width fit shadow-1 bg-blue-grey text-grey-12 rounded-2 q-pa-xs grey-borders">
                  <div class="full-width row q-pa-xs q-pb-sm">
                    <div class="col-8 font-13 text-bold q-pt-xs q-px-xs">
                      Create note
                    </div>
                    <div class="col-4 text-right q-px-xs">
                      <q-btn dense flat icon="cloud_upload" 
                        class="bg-blue-grey text-white q-pa-none q-px-xs font-11"/>
                    </div>
                  </div>
                  <div class="bg-grey-12 q-pa-xs rounded-2 fit">
                    <div class="full-width q-pb-xs">
                      <q-input dense standout="bg-blue-grey text-grey-12" v-model="title" label="Title..." />
                    </div>
                    <q-input
                      v-model="text"
                      autogrow
                      color="blue-grey"
                      class="q-mt-sm"
                    />
                  </div>
                  
                </div>
              </div>
          </div>
          <!-- ADD FILE -->
          <div class="col-6 q-pa-none q-pl-sm" style="min-height: 9em">
              <div class="full-width text-left nasalization font-8 q-pa-none rounded-2">
                <div class="full-width bg-blue-grey shadow-1 rounded-2 q-pa-xs" style="min-height: 14.5em">
                  <q-uploader
                      url="http://localhost:4444/upload"
                      label="Upload file"
                      color="blue-grey"
                      flat
                      class="full-width text-blue-grey bg-grey-12"
                  />
                  <div class="full-width q-pt-xs">
                      <q-input dense standout="bg-blue-grey text-grey-12" v-model="title" label="Rename file..." class="bg-grey-12 rounded-2">
                        <template v-slot:prepend>
                          <q-icon size="xs" name="edit" />
                        </template>
                      </q-input>
                    </div>
                </div>
              </div>
          </div>
        </div>
      </div>
      <div class="full q-pa-none rounded-2 fit">
        <div class="font-8 text-grey-6 q-pt-xs nasalization full-width text-center">
          SAVED ITEMS
        </div>
        <div class="q-pa-none full-width row">
          <!-- LEFT -->
          <div class="col-6 q-pa-none q-pr-xs">
            <div v-for="(note, n) in notes" :key="n" class="full-width q-my-xs">
              <div v-if="n%2 == 0" class="q-pa-xs rounded-2 fit">
                <NoteCard :prop_note="note"></NoteCard>
              </div>
            </div>
          </div>
          <!-- RIGHT -->
          <div class="col-6 q-pa-none q-pl-xs">
            <div v-for="(note, n) in notes" :key="n" class="full-width q-my-xs">
              <div v-if="n%2 != 0" class="q-pa-xs rounded-2 fit">
                <NoteCard :prop_note="note"></NoteCard>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>
  
  <script>
  import { defineComponent, ref } from 'vue'
  import NoteCard from 'src/components/NoteCard.vue'
  
  export default defineComponent({
    components: { NoteCard },
    name: 'NotePad',
    setup () {
      return {
        text: ref(''),
        title: ref(''),
        notes: ref([
          { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note'},
          { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. This note is larger than the previous one'},
          { name: 'Verification.png', type: 'file', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'https://user-images.githubusercontent.com/104391124/248440256-87223a21-37db-4614-b1a7-6e06c94d5b11.png'},
          // { name: 'Poio_1.png', type: 'file', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'https://user-images.githubusercontent.com/52062448/232919052-db06a51e-52e0-488c-939b-88d9f15489da.png'},
          // { name: 'Poio_2.png', type: 'file', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'https://user-images.githubusercontent.com/52062448/232919052-db06a51e-52e0-488c-939b-88d9f15489da.png'},
          { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its content is a little bit larger than the other one :)'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note'},
          // { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'This is a note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'This is another note', type: 'text', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'This is the content of this note. Its larger than the other one :)'},
          // { name: 'Verification.png', type: 'file', direction: 'notes/3cbb7929d81c2d11de022a6', content: 'https://user-images.githubusercontent.com/104391124/248440256-87223a21-37db-4614-b1a7-6e06c94d5b11.png'}
        ])
      }
    }
  })
  </script>
  