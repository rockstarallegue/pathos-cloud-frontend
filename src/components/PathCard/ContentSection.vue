<template>
    <div class="full child container q-pa-none">
        <div class="full child container">
            <!-- INFO BAR -->
            <div class="q-pa-none grey-bottom bg-gral inset-font shadow-1 full-width">
                <!-- INFO BUTTONS -->
                <div class="q-pa-none q-pa-none row">
                    <!-- title -->
                    <div class="col-4 col-md-6 inset-font q-pa-xs rounded-1 text-center">
                        <div class="bg-blue-grey q-pa-none rounded-1">
                            <q-btn flat dense no-caps size="1em" class="q-pa-none text-bold full-width bg-gral q-px-xs">
                                <div :class="($q.platform.is.desktop ? 'font-12' : 'font-6') + 'ellipsis rounded-1 text-dark-blue nasalization q-pa-none'" style="max-width: 400px;">
                                    <q-icon :size="($q.platform.is.desktop ? '1.2em' : '0.9em')" name="route" class="text-dark-blue"></q-icon>
                                    :: {{ title_name }}
                                </div>
                            </q-btn> 
                        </div>
                         
                    </div>
                    <q-separator vertical></q-separator>
                    <!-- actions -->
                    <div class="col-4 col-md-2 q-pa-xs q-px-sm row">
                        <q-btn-group glossy dense spread rounded class="q-pa-none full-width inset-font">
                            <q-btn flat dense square size="xs" icon="share" label="2" class="inset-font q-pa-none" />
                            <q-btn flat dense square size="xs" icon="favorite" label="5" class="inset-font q-pa-none" />
                            <q-btn flat dense square size="xs" icon="bolt" label="1" class="inset-font q-pa-none" />
                        </q-btn-group>
                    </div>
                    <q-separator vertical></q-separator>
                    <!-- rate -->
                    <div class="col-2 q-pa-none text-center col">
                        <div class="col-11 q-px-xs q-pt-xs row">
                            <div class="col-6">
                                <q-btn flat dense spread :color="vote == 1 ? 'lime' : ''" size="xs" :label="rate.up" icon="thumb_up" 
                                class="q-px-none text-dark-blue"
                                @click="rateUp()"
                                />
                            </div>
                            <div class="col-6">
                                <q-btn flat dense spread :color="vote == -1 ? 'pink' : ''" size="xs" :label="rate.down" icon="thumb_down" 
                                class="q-px-none text-dark-blue"
                                @click="rateDown()"
                                />
                            </div>
                        </div>
                        <div class="col-1 q-pa-xs">
                            <div 
                                class="full-width q-pa-none rounded-1" 
                                :style="getRankingLine(rate.up, rate.down)">
                            </div>
                        </div>
                    </div>
                    <q-separator vertical></q-separator>
                    <!-- branch -->
                    <div class="col text-center q-py-xs text-center ">
                        <q-btn push size="sm" dense icon="alt_route" class="text-dark-blue q-pa-xs inset-font"/>
                    </div>
                    <q-separator vertical></q-separator>
                    <!-- pin -->
                    <div class="col text-center q-py-xs text-center ">
                        <q-btn push size="sm" dense icon="push_pin" @click="$emit('pin', node_path)" class="q-pa-xs text-grey-12 q-pa-xs bg-pink-13"/>
                    </div>
                </div>
            </div>
            <!-- CONTENT -->
            <div class="q-pa-none full child container">
                <div class="q-px-xs full child container">
                    <q-scroll-area class="full child container row grey-sides light-2-glass shadow-1">
                        <!-- div class="col-1 q-px-xs bg-teal-11">
                            <PlasmaWrapper></PlasmaWrapper>
                        </div-->
                        <div class="col-11 q-pa-none q-py-none full child container">
                            <div class="q-py-sm q-px-md full child container" style="z-index: 0;">
                                <NodeContainer :node_type="'text'" :prop_node_references="node_references" :prop_node_content="node_text"></NodeContainer>
                                <!-- NodeContainer :node_type="'media'" :prop_node_references="node_references" :prop_node_content="node_text"></NodeContainer-->
                                <NodeContainer :node_type="'frame'" :prop_node_references="node_references" :prop_node_content="'https://www.youtube.com/embed/c0LiwkCbkUM?si=z26dePCxLZ2bGQIc'"></NodeContainer>
                                <NodeContainer :node_type="'text'" :prop_node_references="node_references" :prop_node_content="node_text"></NodeContainer>
                                <!-- blockquote class="twitter-tweet"><p lang="en" dir="ltr">Welcome to the ascension maze. Don’t get confused. <a href="https://t.co/FoLMiUd8pD">pic.twitter.com/FoLMiUd8pD</a></p>&mdash; @goth (@goth600) <a href="https://twitter.com/goth600/status/1702771503534923975?ref_src=twsrc%5Etfw">September 15, 2023</a></blockquote--> 
                                <!-- script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script--> 
                                <!-- NodeContainer :prop_node_references="node_references"></NodeContainer-->
                                <!-- FrameContainer :frame_source="'https://open.spotify.com/embed/track/4pu660BEu16k7ZSbYF16kf'"></FrameContainer>
                                <MediaContainer></MediaContainer>
                                <TextContainer></TextContainer>
                                <FrameContainer :frame_source="'https://www.youtube.com/embed/DbfejwP1d3c?si=-nugH43-0DbszvTn'"></FrameContainer>
                                <FrameContainer :frame_source="'https://www.youtube.com/embed/c0LiwkCbkUM?si=z26dePCxLZ2bGQIc'"></FrameContainer>
                                <MediaContainer></MediaContainer-->
                            </div>
                            
                        </div>
                    </q-scroll-area>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
    import { defineComponent } from 'vue'

    import NodeContainer from 'src/components/PathCard/NodeContainer.vue'

    export default defineComponent({
        components: { NodeContainer },
        name: 'ContentSection',
        data () {
            return {
                rate: { up: 3, down: 1 },
                vote: 0,
                title_name: 'Cool stuff',

                node_text: [
                    { word: 'Lorem', tags: ['word', 'plain'], references:[0] }, 
                    { word: 'ipsum', tags: ['word', 'plain'], references:[1, 2] }, 
                    { word: 'dolor', tags: ['word', 'plain'], references:[] }, 
                    { word: 'sit', tags: ['word', 'plain'], references:[2] }, 
                    { word: 'amet', tags: ['word', 'plain'], references:[1] }, 
                    { word: ',', tags: ['sign', 'plain'], references:[2] }, 
                    { word: 'consectetur', tags: ['word', 'plain'], references:[] }, 
                    { word: 'adipisicing', tags: ['word', 'plain'], references:[] }, 
                    { word: 'elit', tags: ['word', 'plain'], references:[] }, 
                    { word: ',', tags: ['sign', 'plain'], references:[] }, 
                    { word: 'sed', tags: ['word', 'plain'], references:[] }, 
                    { word: 'do', tags: ['word', 'plain'], references:[0, 1, 2] }, { word: 'eiusmod', tags: ['word', 'plain'], references:[] }, { word: 'tempor', tags: ['word', 'plain'], references:[] }, { word: 'incididunt', tags: ['word', 'plain'], references:[] }, { word: 'ut', tags: ['word', 'plain'], references:[] }, { word: 'labore', tags: ['word', 'plain'], references:[] }, { word: 'et', tags: ['word', 'plain'], references:[] }, { word: 'dolore', tags: ['word', 'plain'], references:[] }, { word: 'magna', tags: ['word', 'plain'], references:[] }, { word: 'aliqua', tags: ['word', 'plain'], references:[] }, { word: 'Lorem', tags: ['word', 'plain'], references:[] }, { word: 'ipsum', tags: ['word', 'plain'], references:[] }, { word: 'dolor', tags: ['word', 'plain'], references:[] }, { word: 'sit', tags: ['word', 'plain'], references:[] }, { word: 'amet', tags: ['word', 'plain'], references:[] }, { word: ',', tags: ['sign', 'plain'], references:[] }, { word: 'consectetur', tags: ['word', 'plain'], references:[] }, { word: 'adipisicing', tags: ['word', 'plain'], references:[] }, { word: 'elit', tags: ['word', 'plain'], references:[] }, { word: ',', tags: ['sign', 'plain'], references:[0] }, { word: 'sed', tags: ['word', 'plain'], references:[] }, { word: 'do', tags: ['word', 'plain'], references:[] }, { word: 'eiusmod', tags: ['word', 'plain'], references:[] }, { word: 'tempor', tags: ['word', 'plain'], references:[] }, { word: 'incididunt', tags: ['word', 'plain'], references:[] }, { word: 'ut', tags: ['word', 'plain'], references:[] }, { word: 'labore', tags: ['word', 'plain'], references:[] }, { word: 'et', tags: ['word', 'plain'], references:[] }, { word: 'dolore', tags: ['word', 'plain'], references:[1] }, { word: 'magna', tags: ['word', 'plain'], references:[] }, { word: 'aliqua', tags: ['word', 'plain'], references:[2] }, { word: '.', tags: ['sign', 'plain'] }
                ],
                node_references: [
                    { type: 'Node', author:'@U2', title: 'Pathos', direction: 'nodes/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                    { type: 'Path', author:'@Allegue', title: 'Life Itself', direction: 'paths/a56743cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                    { type: 'Profile', author:'@the_dream_operator', title: 'The Dream Operator', direction: 'profiles/x20943cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                    { type: 'Node', author:'@win_s_hips', title: 'Protein Powder', direction: 'profiles/x20943cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false }
                ],
                node_path: 'nodes/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'
            }
        },
        methods: {
            rateUp () {
                // Removing
                if(this.vote == 1){
                    this.vote = 0;
                    // API update call
                    this.rate.up -=1;
                }
                if(this.vote == -1){
                    this.vote = 1;
                    // API update call
                    this.rate.down -=1;
                    this.rate.up +=1;
                }
                // Actually voting
                else{
                    this.vote = 1;
                    // API update call
                    this.rate.up +=1; 
                }
                
            },
            rateDown () {
                // Removing
                if(this.vote == -1){
                    this.vote = 0;
                    // API update call
                    this.rate.down -=1;
                }
                if(this.vote == 1){
                    this.vote = -1;
                    // API update call
                    this.rate.up -=1;
                    this.rate.down +=1;
                }
                // Actually voting
                else{
                    this.vote = -1;
                    // API update call
                    this.rate.down +=1; 
                }
            },
            getRankingLine(up, down){
                var green = parseInt(up*100/(up+down) - 5)
                var red = parseInt(100 - (down*100/(up+down)) + 5)
                var line = "height:3px; background: linear-gradient(90deg, rgba(205,220,57,1) " + 
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
  