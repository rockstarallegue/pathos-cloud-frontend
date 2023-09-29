<template>
    <div class="full q-pa-none child container">
      <q-card flat class="my-card q-pa-none full child container transparent">
        <q-tab-panels v-model="tab" animated class="full child q-pa-none transparent">
          <q-tab-panel name="tags" label="Tags" class="q-pa-none transparent">
            <TagSection></TagSection>
          </q-tab-panel>
  
          <q-tab-panel name="comments" label="Comments" class="q-pa-none">
            <CommentSection></CommentSection>
          </q-tab-panel>

          <q-tab-panel name="branches" label="Branches" class="q-pa-none">
            <BranchSection></BranchSection>
          </q-tab-panel>

          <!-- q-tab-panel name="origin" label="Branches" class="q-pa-none">
            <OriginSection></OriginSection>
          </q-tab-panel-->
        </q-tab-panels>
        <q-separator></q-separator>
        <div class="q-pa-none q-ma-none">
          <q-toolbar v-if="$q.platform.is.desktop" dense class="q-pa-none q-ma-none">
            <q-tabs dense v-model="tab" class="inset-font q-pa-none q-px-xs nasalization full-width">
              <q-tab dense no-caps icon="label" size="xs" name="tags" class="q-pa-none"/>
              <q-tab dense no-caps icon="forum" size="xs" name="comments" class="q-pa-none"/>
              <q-tab dense no-caps icon="fork_right" size="xs" name="branches" class="q-pa-none"/>
              <!-- q-tab dense no-caps icon="account_tree" size="xs" name="origin"/-->
            </q-tabs>
          </q-toolbar>
          <q-toolbar v-if="$q.platform.is.mobile" dense class="q-pa-none q-ma-none">
            <q-tabs dense v-model="tab" class="inset-font q-pa-none q-px-xs nasalization full-width">
              <q-tab dense icon="label" size="xs" name="tags" class="q-pa-none"/>
              <q-tab dense icon="forum" size="xs" name="comments" class="q-pa-none"/>
              <q-tab dense icon="fork_right" size="xs" name="branches" class="q-pa-none"/>
              <!-- q-tab dense icon="account_tree" size="sm" name="origin"/-->
            </q-tabs>
          </q-toolbar>
        </div>
      </q-card>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  import { ref } from 'vue'

  import CommentSection from 'src/components/PathCard/Actions/CommentSection.vue'
  import BranchSection from 'src/components/PathCard/Actions/BranchSection.vue'
  import TagSection from 'src/components/PathCard/Actions/TagSection.vue'
  
  export default defineComponent({
    components: { TagSection, CommentSection, BranchSection },
    name: 'ActionsSection',
    setup () {
        return {
        tab: ref('comments')
        }
    },
    props: {
      author: {
        type: String,
        required: true
      },
      caption: {
        type: String,
        default: ''
      },
      file: {
        type: String,
        default: ''
      }
    }
  })
  </script>
  