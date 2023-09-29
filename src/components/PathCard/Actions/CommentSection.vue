<template>
    <div class="full q-pa-none transparent">
        <div class="q-pa-none rounded-1 full child container">
            <!-- INFO BUTTONS -->
            <div class="full-width nasalization q-pa-none row">
                <div class="col nasalization inset-font font-9 q-px-md q-pt-sm">
                    Comments
                </div>
                <q-separator vertical></q-separator>
                <div class="col-5 q-pa-none row">
                     <!-- sort -->
                    <div class="text-center q-pa-xs col">
                        <q-btn-dropdown 
                            dense
                            flat
                            style="color: #404258;" 
                            size="xs"
                            icon="sort"
                            label="SORT"
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
                    </div>
                    <q-separator vertical></q-separator>
                    <!-- filter  -->
                    <div class="text-center q-pa-xs col">
                        <q-btn-dropdown 
                            dense
                            flat
                            style="color: #404258;" 
                            size="xs"
                            icon="filter_list"
                            label="FILTER"
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
                    </div>
                </div>
                <q-separator vertical></q-separator>
                <div class="col-2 text-center q-pa-xs">
                    <q-btn push size="md" dense icon="add_comment" class="text-dark-blue q-pa-none q-px-xs inset-font"/>
                </div>
            </div>
            <q-separator></q-separator>
            <!-- COMMENTS -->
            <div class="fit q-pa-none">
                <q-scroll-area flat class="full child container rounded-2">
                    <div class="full q-pa-sm">
                        <div 
                            v-for="(tag, n) in tags_array" 
                            :key="n"
                            class="q-pa-none q-mb-sm"
                        >
                            <!-- div class="q-pa-none grey-border-3 row rounded-2"-->
                                <div class="col-10 q-pa-none rounded-2 full child container">
                                    <div class="fit row q-pa-sm">
                                        <CommentNester :enabled="false"/>
                                    </div>
                                </div>
                            <!--/div-->
                        </div>
                    </div>
                </q-scroll-area>
            </div>
            
        </div>
    </div>
</template>

<script>
import { defineComponent } from 'vue'
import CommentNester from 'src/components/PathCard/Actions/Nesters/CommentNester.vue'

export default defineComponent({
  components: { CommentNester },
  name: 'CommentSection',
  data () {
      return {
          enabled: 2,
          tags_array: [
              { taglist: ['GIF', 'Visual', 'Media Types', 'Content', 'Pathos Tags'], enabled: 3, pos: 0, ranked: 0.3 },
              { taglist: ['Pixel Art', 'Art Categories', 'Pathos Tags'], enabled: 1, pos: 0, ranked: 0.4 },
              { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, ranked: 0.5 }
          ]
      }
  },
  methods: {
      enableFather (n) {
          this.tags_array[n].enabled = (this.tags_array[n].enabled < (this.tags_array[n].taglist.length - 1)) ? this.tags_array[n].enabled + 1 : (this.tags_array[n].taglist.length - 1);
          this.enabled += 1;
      },
      disableFather (n) {
          this.tags_array[n].enabled = (this.tags_array[n].enabled > 0) ? this.tags_array[n].enabled - 1 : 0;
          this.enabled -= 1;
          // console.log("to ", this.tags_array[n].enabled)
      }
  }
})
</script>