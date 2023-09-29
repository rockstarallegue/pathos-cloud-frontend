<template>
    <div class="full child container rounded-2">
        <div class="font-8 row rounded-1 light-1-glass q-pa-none rounded-2 grey-border-3">
            <!-- INFO BUTTONS -->
            <div class="full-width q-pa-none row">
                <!-- User information -->
                <div class="col-10 col-md-11 row">
                    <!-- q-separator vertical></q-separator-->
                    <div class="col q-pa-xs">
                        <q-btn rounded no-caps align="left" class="font-9 q-pa-none q-px-xs text-dark-blue text-bold bg-grey-12 full-width">
                            <div class="ellipsis q-pa-none">
                                <q-icon size="1.3em" name="face_5"></q-icon>
                                :: {{ author.username }}
                            </div>
                            <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                                <div class="text-center text-black">
                                    {{ author.username }}
                                </div>
                                {{ author.userpath }}
                            </q-tooltip>
                        </q-btn>
                    </div>
                    <div class="col-3 col-md-2 q-px-xs q-pt-sm">
                        <span class="text-dark-blue font-8 nasalization"> [{{ date[0] }}]</span>
                    </div>
                    <!-- q-separator vertical></q-separator-->
                    <div class="col-4 col-md-5 q-px-xs q-pt-xs">
                        <CredentialTagScroll></CredentialTagScroll>
                    </div>
                </div>
                <!-- q-separator vertical></q-separator-->
                <!-- Buttons -->
                <div class="col q-pa-none row">
                     <!-- SEARCH -->
                    <div class="text-center q-py-xs col">
                        <q-btn
                            flat dense style="color: #404258;" size="xs" icon="location_searching" 
                            class="nasalization full-width inset-font q-pa-xs"
                            @click="switchToSearchMode()"
                        />
                    </div>
                    <!-- q-separator vertical></q-separator-->
                    <!-- REFERENCES -->
                    <div class="text-center q-py-xs col">
                        <q-btn
                            flat dense style="color: #404258;" size="xs" icon="summarize" 
                            class="nasalization full-width inset-font q-pa-xs"
                            @click="showAllReferences()"
                        >
                        <q-badge color="grey-12" class="text-dark-blue q-pa-none q-px-xs" floating>{{ comment_references.length }}</q-badge>
                        </q-btn>
                    </div>
                </div>
            </div>
            <!-- q-separator></q-separator-->
            <!-- TEXT -->
            <div class="full-width q-pa-none row">
                <!-- q-separator vertical></q-separator-->
                <!-- q-separator></q-separator-->
                <div class="fit q-pa-xs">
                    <!-- q-separator vertical></q-separator-->
                    <div class="flex justify-around bg-grey-12 q-pa-none rounded-2">
                        <!-- q-separator vertical></q-separator-->
                        <div v-if="search_mode === true" class="flex justify-around rounded-2 q-pa-xs">
                            <q-btn
                                v-for="(word_obj, n) in comment_text" 
                                :key="n"
                                flat
                                dense
                                no-caps
                                :label="word_obj.word" 
                                size="sm"
                                :class="referencedStyle(word_obj.references)"
                                @click="showReferences(word_obj.references)"
                            />
                        </div>
                        <div v-if="search_mode === false" class="flex justify-around rounded-2 q-pa-xs dark-blue">
                            <q-btn
                                v-for="(word_obj, n) in comment_text" 
                                :key="n"
                                icon="adjust"
                                size="xs"
                                dense
                                no-caps 
                                :label="word_obj.word" 
                                class="q-px-sm q-ml-xs q-mt-xs bg-grey-13 text-dark-blue nasalization inset-font"
                            />
                        </div>
                    </div>
                </div>
            </div>
            <!-- q-separator></q-separator-->
            <!-- REFERENCES -->
            <div v-if="show_references == true" class="full-width q-pa-none row">
                <!-- q-separator vertical></q-separator-->
                <!-- q-separator></q-separator-->
                <div class="fit q-pa-xs">
                    <!-- q-separator vertical></q-separator-->
                    <div class="light-1-glass q-pa-none rounded-2">
                        <!-- q-separator vertical></q-separator-->
                        <div class="rounded-2 q-pa-xs">
                            <div class="full-width row">
                                <div class="col-9 col-md-10">
                                    <span class="nasalization font-9 text-dark-blue q-px-xs q-pb-xs">References</span>
                                </div>
                                <div class="col full-width text-right row">
                                     <!-- sort -->
                                    <div class="q-pa-none col">
                                        <q-btn-dropdown 
                                            dense
                                            flat
                                            size="xs"
                                            icon="sort"
                                            class="q-px-xs text-dark-blue"  
                                        >
                                            <q-list>
                                                <q-item clickable v-close-popup @click="onItemClick">
                                                    <q-item-section>
                                                    <q-item-label>Die</q-item-label>
                                                    </q-item-section>
                                                </q-item>
                                            </q-list>
                                        </q-btn-dropdown>
                                    </div>
                                    <!-- filter  -->
                                    <div class="q-pa-none col">
                                        <q-btn-dropdown 
                                            dense
                                            flat
                                            size="xs"
                                            icon="filter_list"
                                            class="q-px-xs text-dark-blue"  
                                        >
                                            <q-list>
                                                <q-item clickable v-close-popup @click="onItemClick">
                                                    <q-item-section>
                                                    <q-item-label>Die</q-item-label>
                                                    </q-item-section>
                                                </q-item>
                                            </q-list>
                                        </q-btn-dropdown>
                                    </div>
                                </div>
                            </div>
                            
                            <div 
                                v-for="(reference, r) in comment_references" 
                                class="full-width nasalization text-dark-blue" :key="r"
                            >
                            <div v-if="reference.enabled == true" class="full-width q-py-xs">
                                <q-btn dense rounded no-caps align="left" :icon="referenceIcon(reference.type)"
                                    class="font-8 q-px-xs text-dark-blue full-width bg-grey-12">
                                    <div class="ellipsis q-px-xs text-grey-8">
                                        {{ reference.author }} - <span class="text-dar-blue">{{ reference.title }}</span>
                                    </div>
                                    <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                                        {{ reference.direction }}
                                    </q-tooltip>
                                </q-btn>
                                </div>
                            </div>
                            <div class="full-width">
                                <q-btn flat dense no-caps 
                                    size="sm" 
                                    label="Hide references" 
                                    icon-right="expand_less" 
                                    class="q-px-sm full-width text-dark-blue nasalization text-bold"
                                    @click="hideReferences()"
                                />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- INTERACTION -->
            <!-- q-separator></q-separator-->
            <div class="font-8 row rounded-1 q-pa-none full-width">
                <!-- q-separator vertical></q-separator-->
                <!-- Social -->
                <div class="col-3 col-md-3 q-px-xs full">
                    <q-btn-group glossy rounded dense spread class="q-pa-none grey-square inset-font">
                        <q-btn flat dense square size="xs" icon="share" class="inset-font q-pa-none" />
                        <q-btn flat dense square size="xs" icon="favorite" class="inset-font q-pa-none" />
                        <q-btn flat dense square size="xs" icon="bolt" class="inset-font q-pa-none" />
                    </q-btn-group>
                </div>
                <!-- Rate -->
                <div class="col-2 col-md-3 full q-pa-none text-center row">
                    <div class="col-6 text-center">
                        <q-btn flat dense spread :color="vote == 1 ? 'lime-13' : ''" size="xs" :label="rate.up" icon="thumb_up" 
                        class="q-px-xs text-dark-blue"
                        @click="rateUp()"
                        />
                    </div>
                    <div class="col-6 text-center">
                        <q-btn flat dense spread :color="vote == -1 ? 'red-13' : ''" size="xs" :label="rate.down" icon="thumb_down" 
                        class="q-px-xs text-dark-blue"
                        @click="rateDown()"
                        />
                    </div>
                </div>
                <!-- q-separator vertical></q-separator-->
                <!-- Replies -->
                <div class="col-7 col-md-6 text-center row">
                    <div class="col-6 text-right q-px-xs">
                        <q-btn flat dense no-caps 
                            size="sm" 
                            :label="comments.length.toString() + ' replies'" 
                            :icon-right="expand_comments == true ? 'expand_less' : 'expand_more'" 
                            class="q-px-sm nasalization text-dark-blue text-right"
                            @click="expandComments()"
                        />
                    </div>
                    <!-- q-separator vertical></q-separator-->
                    <div class="col-6 text-right full-length q-px-xs q-pb-xs">
                        <q-btn push dense no-caps 
                            size="xs"
                            label="REPLY" 
                            icon="forum" 
                            class="inset-font q-pa-xs nasalization text-dark-blue bg-grey-12"
                            @click="expandComments()"
                        />
                        <q-btn push dense no-caps 
                            size="xs"
                            icon="push_pin"
                            class="q-pa-xs q-ml-sm text-grey-12 bg-pink-13"
                        />
                    </div>
                </div>
            </div>
        </div>
        <!-- EXPAND COMMENTS -->
        <div v-if="expand_comments == true" class="full-width q-pr-xs q-py-xs q-pl-md">
            <!-- q-separator></q-separator-->
            <div class="full-width rounded-2 light-1-glass grey-border-3 q-pa-xs">
                <!-- q-separator vertical></q-separator-->
                <div class="full-width row">
                    <div class="col-8 col-md-10">
                        <span class="nasalization font-7 text-dark-blue q-px-xs q-pb-xs">Replies</span>
                    </div>
                    <div class="col full-width text-right row">
                            <!-- sort -->
                        <div class="q-pa-none col">
                            <q-btn-dropdown 
                                dense
                                flat
                                size="xs"
                                icon="sort"
                                class="q-px-xs text-dark-blue"  
                            >
                                <q-list>
                                    <q-item clickable v-close-popup @click="onItemClick">
                                        <q-item-section>
                                        <q-item-label>Die</q-item-label>
                                        </q-item-section>
                                    </q-item>
                                </q-list>
                            </q-btn-dropdown>
                        </div>
                        <!-- filter  -->
                        <div class="q-pa-none col">
                            <q-btn-dropdown 
                                dense
                                flat
                                size="xs"
                                icon="filter_list"
                                class="q-px-xs text-dark-blue"  
                            >
                                <q-list>
                                    <q-item clickable v-close-popup @click="onItemClick">
                                        <q-item-section>
                                        <q-item-label>Die</q-item-label>
                                        </q-item-section>
                                    </q-item>
                                </q-list>
                            </q-btn-dropdown>
                        </div>
                    </div>
                </div>
                <div v-for="(comment, c) in comments" :key="c" class="full-width q-pb-xs rounded-2">
                    <!-- q-separator vertical></q-separator-->
                    <CommentNester :enabled="false"></CommentNester>
                </div>
            </div>
        </div>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  import CredentialTagScroll from 'src/components/CredentialTagScroll.vue'
  
  export default defineComponent({
    components: { CredentialTagScroll },
    name: 'CommentNester',
    data () {
        return {
            enabled_flag: this.enabled,
            pos_flag: this.pos,

            search_mode: true,
            show_references: false,
            word_style: "q-pa-none q-ml-xs disabled",
            sign_style: "q-pa-none disabled",

            // COMMENT STRUCTURE
            rate: { up: 3, down: 1 },
            vote: 0,
            date: ['3 days ago', 'Fri 31 Sep 2023 5:10:33'],
            comment_text: [
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
            comment_references: [
                { type: 'Node', author:'@U2', title: 'Pathos', direction: 'nodes/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                { type: 'Path', author:'@Allegue', title: 'Life Itself', direction: 'paths/a56743cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                { type: 'Profile', author:'@the_dream_operator', title: 'The Dream Operator', direction: 'profiles/x20943cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false },
                { type: 'Node', author:'@win_s_hips', title: 'Protein Powder', direction: 'profiles/x20943cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', enabled: false }
            ],
            author: { 
                username: 'mr_dreaminator --e/acc sdndnk', 
                userpath: 'users/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                credentials: [
                    { type: 'Profile', title: 'Twitter profile', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] },
                    { type: 'Community', title: 'Visual Artists', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] },
                    { type: 'Organisation', title: 'UAEM', direction: 'https://twitter.com/ll3gu3', avatar: '', milestones: [ { title: 'Handball team student', direction: 'milestones/b93cbb7929' }, { title: 'High School diploma', direction: 'milestones/n73cbb7929'} ] }
                ]
            },
            comments:[
                'comments/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                'comments/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'
            ],
            expand_comments: this.enabled
        }
    },
    methods: {
        wordSpace (word_obj) {
            if(word_obj.tags[0] == "word"){
                return this.word_style
            }
            else{
                return this.sign_style
            }
        },
        switchToSearchMode () {
            if(this.search_mode == true) {
                this.search_mode = false;
                this.word_style = "q-pa-none q-ml-xs disabled"
            } else {
                this.search_mode = true
                this.word_style = "q-px-xs q-ml-xs q-mt-xs bg-grey-13 text-grey-11 nasalization borders-1"
            }
        },
        expandComments () {
            if(this.expand_comments == true) {
                this.expand_comments = false;
            } else {
                this.expand_comments = true
            }
        },
        copyPath () {
            this.$refs.myinput.focus();
            document.execCommand('copy');
        },
        referencedStyle (references = []) {
            if(references.length > 0) { return 'q-pa-none q-ml-xs underline-word-btn'; }
            else{
               return 'q-pa-none q-ml-xs word-btn disabled';
            } 
        },
        showReferences (refs = []) {
            this.show_references = true;
            // SHUTTING OFF EVERYTHING
            for(let i=0; i<this.comment_references.length; i++){
                this.comment_references[i].enabled = false;
            }
            for(let i=0; i<refs.length; i++){
                this.comment_references[refs[i]].enabled = true;
            }
            
        },
        showAllReferences () {
            this.show_references = this.show_references == true ? false : true;
            for(let i=0; i<this.comment_references.length; i++){
                this.comment_references[i].enabled = true;
            }
        },
        hideReferences () {
            this.show_references = false;
            for(let i=0; i<this.comment_references.length; i++){
                this.comment_references[i].enabled = false;
            }
        },
        referenceIcon (type) {
            if(type == 'Path') { return 'route'; }
            if(type == 'Tag') { return 'label_important'; }
            if(type == 'Profile') { return 'face_5'; }
            if(type == 'Community') { return 'diversity_2'; }
            if(type == 'Organisation') { return 'reduce_capacity'; }
            if(type == 'Hypermarket') { return 'shopping_basket'; }
            else { return 'adjust'; }
        },
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
        }
    },
    props: {
        enabled: {}
    }
  })
  </script>
  