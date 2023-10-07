<template>
    <div class="q-pa-none shadow-2 blue-grey-square rounded-2">
        <div class="bg-grey-12 q-pa-none rounded-2 fit">
            <div v-if="note.type == 'text'" class="full-width q-pa-none">
                <q-input dense standout="bg-blue-grey text-grey-12" v-model="note.name"/>
            </div>
            <q-input
                v-if="note.type == 'text'"
                v-model="note.content"
                square
                dense
                autogrow
                color="blue-grey"
                standout="bg-blue-grey text-grey-12"
            />
            <div
                v-if="note.type == 'file'"
                class="wrap rounded-1 q-pa-xs bg-grey-12 text-center full child">
                <q-img
                    :src="note.content"
                    class="rounded-1 full-width"
                    fit="mode"
                >
                <div class="absolute-bottom text-subtitle1 text-center">
                    <div class="full-width q-pa-none text-white">
                    <q-input dense dark color="blue-grey" filled v-model="note.name">
                    </q-input>
                    </div>
                </div>
                </q-img>
            </div>
            <div class="full-width q-pa-xs bg-blue-grey row">
                <div class="col-10 col-md-9">
                    <q-btn push :size="$q.platform.is.desktop ? 'sm' : 'xs'" icon="adjust" class="text-blue-grey text-bold bg-gral nasalization full-width" label="Nodify"></q-btn>
                </div>
                <div class="col-2 col-md-3 q-pl-xs">
                    <q-btn push :size="$q.platform.is.desktop ? 'sm' : 'xs'" icon="delete" class="text-brown bg-gral nasalization full-width"></q-btn>
                </div>
            </div>
        </div>
    </div>
    
</template>
  
 <script>
  import { defineComponent, ref } from 'vue'

  var the_note = ''
  var note = ''
  export default defineComponent({
    name: 'NoteCard',

    data() {
        return {
            // the_note: ''
            //this_note: this.prop_note
        }
    },
    setup () {
      return {
        text: ref(''),
        title: ref(''),
        note: ref(the_note)
      }
    },
    methods: {
        getNote () {
            this.the_note = this.prop_note
            this.note = this.prop_note
            // console.log('NOTE: ', this.the_note.name)
            // return this.prop_note
        }
    },
    mounted () {
        this.getNote()
    },
    props: {
        prop_note: {}
    }
  })
  </script>
  