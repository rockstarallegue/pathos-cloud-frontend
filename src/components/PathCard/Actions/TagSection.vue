<template>
    <div class="full q-pa-none transparent">
        <div class="q-pa-none rounded-1 full child container">
            <!-- INFO BUTTONS -->
            <div class="full-width q-pa-none row">
                <div class="col nasalization inset-font font-8 q-px-md q-pt-sm">
                    Tags
                </div>
                <q-separator vertical></q-separator>
                <div class="col-5 q-pa-none row nasalization">
                     <!-- sort -->
                    <div class="text-center q-pa-xs col">
                        <q-btn-dropdown 
                            dense
                            flat
                            style="color: #404258;" 
                            size="xs"
                            icon="sort"
                            label="SORT"
                            class="q-px-xs inset-font"  
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
                            class="q-px-xs inset-font"  
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
                    <q-btn push size="md" dense icon="new_label" class="text-dark-blue q-pa-none q-px-xs inset-font"/>
                </div>
            </div>
            <q-separator></q-separator>
            <!-- TAGS -->
            <div class="fit q-pa-sm rounded-2">
                <q-scroll-area flat class="full child container rounded-2">
                    <div class="full rounded-2">
                        <div 
                            v-for="(tag, n) in tags_array" 
                            :key="n"
                            class="q-pa-sm"
                        >
                            <div class="q-pa-none light-1-glass grey-border-3 row rounded-2">
                                <div class="col-10 q-pa-none full rounded-2 child container">
                                    <div class="full-width row">
                                        <div class="col-7 col-md-6 q-pa-none row">
                                            <div class="col q-pa-xs text-center">
                                                <q-btn
                                                    flat rounded size="sm" icon="label_important" 
                                                    class="nasalization bg-grey-12 inset-font q-pa-xs"
                                                />
                                            </div>
                                            <q-separator vertical></q-separator>
                                            <div class="col-9 q-pa-xs text-center">
                                                <q-btn flat color="primary" size="sm" class="bg-grey-12 text-black full-width">
                                                    <div class="ellipsis">
                                                    {{ tag.taglist[tag.enabled] }}
                                                    </div>
                                                </q-btn>
                                            </div>
                                        </div>
                                        <q-separator vertical></q-separator>
                                        <!-- EXPLORING BUTTON -->
                                        <div class="col text-center q-pa-xs">
                                            <q-btn
                                                flat
                                                dense
                                                style="color: #404258;" 
                                                size="xs" 
                                                icon="search" 
                                                :label="$q.platform.is.desktop == true ? 'Father' : ''" 
                                                class="nasalization inset-font"
                                                @click="enableFather(n)"
                                            />
                                        </div>
                                        <q-separator vertical></q-separator>
                                        <div class="col text-center q-pa-xs">
                                            <q-btn
                                                flat
                                                dense
                                                style="color: #404258;" 
                                                size="xs"
                                                icon="keyboard_return"
                                                :label="$q.platform.is.desktop == true ? 'Back to son' : ''"
                                                class="nasalization inset-font"
                                                @click="disableFather(n)"
                                            />
                                        </div>
                                    </div>
                                    <q-separator></q-separator>
                                    <div class="fit row q-pa-xs rounded-1">
                                        <div class="q-pa-xs full-width rounded-2" :style="getRankingBackground(tag.up, tag.down)">
                                            <div class="q-pa-none rounded-1 full-width">
                                                <TagNester v-if="tag.enabled > 0" :taglist="tag.taglist" :enabled="tag.enabled" :pos="tag.pos + 1"/>
                                            </div>
                                            <!-- div class="q-pa-xs rounded-1 full-width">
                                                <div 
                                                    class="full-width q-pa-none rounded-1" 
                                                    :style="getRankingBackground(tag.up, tag.down)">
                                                </div>
                                            </div-->
                                        </div>
                                    </div>
                                </div>
                                <q-separator vertical></q-separator>
                                <!-- Rate -->
                                <div class="col col-md-1 full q-pa-xs text-center column">
                                    <div class="full-width q-pa-xs">
                                        <q-btn flat dense spread :color="tag.vote == 1 ? 'lime' : '#474E68'" size="xs" :label="tag.up" icon="thumb_up" class="text-dark-blue" @click="rateUp(n)"/>
                                    </div>
                                    <div class="full-width q-pa-xs">
                                        <q-btn flat dense spread :color="tag.vote == -1 ? 'pink' : '#474E68'" size="xs" :label="tag.down" icon="thumb_down" class="text-dark-blue" @click="rateDown(n)"/>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                </q-scroll-area>
            </div>
            
        </div>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  import TagNester from 'src/components/PathCard/Actions/Nesters/TagNester.vue'
  
  export default defineComponent({
    components: { TagNester },
    name: 'TagSection',
    data () {
        return {
            enabled: 2,
            tags_array: [
                { taglist: ['GIF', 'Visual', 'Media Types', 'Content', 'Pathos Tags'], enabled: 0, pos: 0, up: 1, down: 3, vote: 0 },
                { taglist: ['Pixel Art', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 10, down: 13, vote: 1},
                { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 5, down: 2, vote: -1 },
                { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 5, down: 2, vote: -1 },
                { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 5, down: 2, vote: -1 },
                { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 5, down: 2, vote: -1 },
                { taglist: ['RGB', 'Art Categories', 'Pathos Tags'], enabled: 0, pos: 0, up: 5, down: 2, vote: -1 }
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
        },
        rateUp (n) {
            // Removing
            if(this.tags_array[n].vote == 1){
                this.tags_array[n].vote = 0;
                // API update call
                this.tags_array[n].up -=1;
            }
            if(this.tags_array[n].vote == -1){
                this.tags_array[n].vote = 1;
                // API update call
                this.tags_array[n].down -=1;
                this.tags_array[n].up +=1;
            }
            // Actually voting
            else{
                this.tags_array[n].vote = 1;
                // API update call
                this.tags_array[n].up +=1; 
            }
            
        },
        rateDown (n) {
            // Removing
            if(this.tags_array[n].vote == -1){
                this.tags_array[n].vote = 0;
                // API update call
                this.tags_array[n].down -=1;
            }
            if(this.tags_array[n].vote == 1){
                this.tags_array[n].vote = -1;
                // API update call
                this.tags_array[n].up -=1;
                this.tags_array[n].down +=1;
            }
            // Actually voting
            else{
                this.tags_array[n].vote = -1;
                // API update call
                this.tags_array[n].down +=1; 
            }
        },
        getRankingBackground(up, down){
            var green = parseInt(up*100/(up+down) - 5)
            var red = parseInt(100 - (down*100/(up+down)) + 5)
            var line = "background: linear-gradient(90deg, rgba(205,220,57,1) " + 
            green.toString() +
            "%, rgba(233,30,99,1) " + 
            red.toString() +
            "%);";
            // console.log("line: ", line)
            return line
        }
    }
  })
  </script>
  