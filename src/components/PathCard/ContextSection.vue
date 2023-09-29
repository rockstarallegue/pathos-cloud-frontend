<template>
  <div class="column q-pa-none fit">
    <div class="col-12 q-pa-none fit">
      <div class="row q-px-xs inset-font nasalization full child">
          <!-- div v-if="$q.platform.is.desktop" class="col-12 full-width" style="height: 0.2em;"></div-->
          <!-- VERIFIED -->
          <div class="col-12 col-md-5 q-pa-none full child">
            <div class="row q-py-xs q-pr-sm full child">
              <div class="q-pa-none">
                <q-btn-dropdown 
                    dense
                    flat
                    rounded
                    style="color: #404258;" 
                    size="sm"
                    icon="check_circle"
                    class="q-pa-xs inset-font"  
                >
                    <q-list>
                    <q-item clickable v-close-popup @click="onItemClick">
                        <q-item-section>
                        <q-item-label>Die</q-item-label>
                        </q-item-section>
                    </q-item>

                    <q-item clickable v-close-popup @click="onItemClick">
                        <q-item-section>
                        <q-item-label>Live forever</q-item-label>
                        </q-item-section>
                    </q-item>
                    </q-list>
                </q-btn-dropdown>
                <!-- q-btn rounded flat class="inset-font" size="sm" icon="check_circle">
                  <q-tooltip class="bg-black text-grey-11">Verified tags</q-tooltip>
                </q-btn-->
              </div>
              <div v-if="$q.platform.is.desktop" class="col light-1-glass rounded-2 q-pa-xs grey-border-3 rounded-1">
                <VerifiedTagScroll></VerifiedTagScroll>
              </div>
              <div v-if="$q.platform.is.mobile" class="col light-1-glass rounded-2 tag-padding grey-border-3 rounded-1">
                <VerifiedTagScroll></VerifiedTagScroll>
              </div>
            </div>
          </div>
          
          <!-- RANKED -->
          <div class="col-12 col-md-7 q-pa-none full child">
            <div class="row q-py-xs q-pr-sm full child">
              <div class="q-pa-none">
                <q-btn-dropdown 
                    dense
                    flat
                    rounded
                    style="color: #404258;" 
                    size="sm"
                    icon="stars"
                    class="q-pa-xs inset-font"  
                >
                    <q-list>
                    <q-item clickable v-close-popup @click="onItemClick">
                        <q-item-section>
                        <q-item-label>Die</q-item-label>
                        </q-item-section>
                    </q-item>

                    <q-item clickable v-close-popup @click="onItemClick">
                        <q-item-section>
                        <q-item-label>Live forever</q-item-label>
                        </q-item-section>
                    </q-item>
                    </q-list>
                </q-btn-dropdown>
                <!--q-btn rounded flat class="inset-font" size="sm" icon="stars">
                  <q-tooltip class="bg-black text-grey-11">Ranked tags</q-tooltip>
                </q-btn-->
              </div>
              <div v-if="$q.platform.is.desktop" class="col light-1-glass rounded-2 q-pa-xs grey-border-3 rounded-1">
                <RankedTagScroll></RankedTagScroll>
              </div>
              <div v-if="$q.platform.is.mobile" class="col light-1-glass rounded-2 tag-padding grey-border-3 rounded-1">
                <RankedTagScroll></RankedTagScroll>
              </div>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>
  
<script>
  import { defineComponent } from 'vue'
  import VerifiedTagScroll from 'src/components/VerifiedTagScroll.vue'
  import RankedTagScroll from 'src/components/RankedTagScroll.vue'
  
  export default defineComponent({
    components: { VerifiedTagScroll, RankedTagScroll },
    name: 'ContextSection',
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
  