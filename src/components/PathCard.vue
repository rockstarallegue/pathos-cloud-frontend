<template>
    <div class="full child container q-pa-none">
      <div class="column full child q-pa-none">
        <!-- POST CONTEXT -->
        <div class="q-pa-none full-width row bg-gral">
          <!-- AuthorContext></AuthorContext-->
          <div class="col-12 col-md-4">
            <AuthorContext></AuthorContext>
          </div>
          <div class="col-12 col-md-8">
            <ContextSection></ContextSection>
          </div>
        </div>
        <q-separator></q-separator>
        <!-- CONTENT AND ACTIONS -->
        <div class="child q-pa-none tag-padding shadow-1">
          <!-- DESKTOP DESIGN -->
          <div v-if="$q.platform.is.desktop" class="row full child grey-sides-v">
            <div class="col-7 q-pa-none full child">
              <ContentSection @pin="(pin) => $emit('pin', pin)"></ContentSection>
            </div>
            <!-- q-separator vertical></q-separator-->
            <div class="col-4 q-pa-none grey-sides full child bg-gral">  
              <ActionsSection></ActionsSection>
            </div>
          </div>
  
          <!-- MOBILE DESIGN -->
          <div v-if="$q.platform.is.mobile" class="column full child">
            <div class="col-7 q-pa-none full child">
              <ContentSection></ContentSection>
            </div>
            <div class="col-5 q-pa-none full child bg-gral">
              <q-separator></q-separator>
              <ActionsSection></ActionsSection>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { defineComponent } from 'vue'
  import { ref } from 'vue'
  import ActionsSection from 'src/components/PathCard/ActionsSection.vue'
  import ContextSection from 'src/components/PathCard/ContextSection.vue'
  import AuthorContext from 'src/components/PathCard/AuthorContext.vue'
  import ContentSection from 'src/components/PathCard/ContentSection.vue'
  
  export default defineComponent({
    components: { ActionsSection, ContextSection, ContentSection, AuthorContext },
    // components: { AuthorContext, ContentSection, ActionsSection },
    name: 'PathCard',
    setup () {
        return {
        tab: ref('tags')
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
  