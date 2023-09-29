<template>
    <div class="rounded-borders bordered hidden-overflow">
        <div class="full-height text-grey-7">
            <q-editor
                v-model="editor"
                ref="editorRef"
                toolbar-text-color="blue-grey"
                toolbar-toggle-color="yellow-8"
                toolbar-bg="grey-12"
                :toolbar="[
                    ['token'],
                    ['bold', 'italic', 'underline'],
                    [{
                    label: $q.lang.editor.formatting,
                    icon: $q.iconSet.editor.formatting,
                    list: 'no-icons',
                    options: ['p', 'h3', 'h4', 'h5', 'h6', 'code']
                    }]
                ]"
                class="full-height bg-grey-12"
            >
            <template v-slot:token>
                <q-btn-dropdown
                dense no-caps
                ref="tokenRef"
                no-wrap
                unelevated
                color="white"
                text-color="blue-grey"
                label="Reference list"
                size="sm"
                class="nasalization font-8"
                >
                <q-list dense>
                    <q-item tag="path" clickable @click="add('This is a path link')">
                        <q-item-section side>
                            <q-icon name="route" />
                        </q-item-section>
                        <q-item-section>Path</q-item-section>
                    </q-item>
                    <q-item tag="node" clickable @click="add('This is a node link')">
                        <q-item-section side>
                            <q-icon name="adjust" />
                        </q-item-section>
                        <q-item-section>Node</q-item-section>
                    </q-item>
                    <q-item tag="profile" clickable @click="add('This is a profile link')">
                        <q-item-section side>
                            <q-icon name="face_5" />
                        </q-item-section>
                        <q-item-section>Profile</q-item-section>
                    </q-item>
                </q-list>
                </q-btn-dropdown>
            </template>
            </q-editor>
        </div>
    </div>
</template>
<style lang="sass">
.editor_token
  background: rgba(0, 0, 0, .6)
  color: white
  padding: 3px
  &, .q-icon
    border-radius: 3px
  .q-icon
    background: rgba(0, 0, 0, .2)
</style>
<script>
import { ref, defineComponent } from 'vue'

export default defineComponent({
  name: 'NoteBox',
  setup () {
    const editorRef = ref(null)
    const tokenRef = ref(null)

    return {
      editorRef,
      tokenRef,
      editor: ref(''),

      add (name) {
        const edit = editorRef.value
        tokenRef.value.hide()
        edit.caret.restore()
        edit.runCmd('insertHTML', `&nbsp;<div class="editor_token row inline items-center" contenteditable="false">&nbsp;<span>${name}</span>&nbsp;<i class="q-icon material-icons cursor-pointer" onclick="this.parentNode.parentNode.removeChild(this.parentNode)">close</i></div>&nbsp;`)
        edit.focus()
      }
    }
  },
  props: {
    icon: {
      type: String,
      required: false
    },
    title: {
      type: String,
      required: false
    }
  }
})
</script>
