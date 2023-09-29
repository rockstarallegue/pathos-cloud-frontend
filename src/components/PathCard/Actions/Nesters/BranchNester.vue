<template>
    <div class="full child container rounded-1 q-pa-none">
        <div class="font-8 column rounded-1 q-pa-none grey-border-3">
            <!-- INFO BUTTONS -->
            <div class="full-width q-pa-none row">
                <!-- User information -->
                <div class="col-12 col-md-11 q-pa-none row">
                    <div class="col-1 q-pa-xs text-center">
                        <q-btn 
                            dense
                            rounded
                            size="sm" 
                            icon="route"
                            class="q-pa-xs text-dark-blue inset-font bg-grey-12">
                        </q-btn>
                    </div>
                    <q-separator vertical></q-separator>
                    <div class="col-3 col-md-4 q-pa-xs">
                        <q-btn rounded no-caps align="left" class="font-9 q-pa-none q-px-sm text-dark-blue text-bold bg-grey-12 full-width">
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
                    <div class="col q-pa-xs q-pt-sm">
                        <span class="text-dark-blue font-8 nasalization"> [{{ date[0] }}]</span>
                    </div>
                    <!-- q-separator vertical></q-separator-->
                    <div class="col-5 q-pa-xs">
                        <CredentialTagScroll></CredentialTagScroll>
                    </div>
                </div>
                <!-- q-separator vertical></q-separator-->
            </div>
            <q-separator></q-separator>
            <!-- NAME -->
            <div class="full-width q-px-sm rounded-2 row">
                <div class="col-8 ellipsis text-dark-blue nasalization">
                    <q-icon name="route"></q-icon>
                    :: This is a branch that doesn't make sense
                </div>
                <q-separator vertical></q-separator>
                <div class="col text-grey nasalization text-center">
                    <q-icon name="content_copy"></q-icon>
                    :: V 0.0.0
                </div>
                <q-separator vertical></q-separator>
                <div class="col-1 text-grey nasalization text-center">
                    <div class="q-pa-none col">
                        <q-btn-dropdown 
                            dense
                            flat
                            size="xs"
                            icon="history"
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
            <q-separator></q-separator>
            <!-- PATH CONTAINER -->
            <div class="full-width q-pa-xs rounded-2">
                <!-- q-separator vertical></q-separator-->
                <div class="q-pa-none fit neon-surface rounded-2" style="min-height: 140px;">
                    <q-scroll-area class="q-pa-xs q-py-xs fit light-2-glass rounded-2">
                        <div class="row no-wrap">
                            <div v-for="(node, n) in branch_nodes" :key="n" class="rounded-1 q-mr-sm row" style="max-width: 210px;">
                                <div class="rounded-1 light-1-glass grey-border-3 q-pa-none">
                                    <div class="q-pa-xs text-left">
                                        <q-btn flat color="primary" size="xs" class="bg-grey-12 text-black q-px-xs full">
                                            <div class="ellipsis">
                                            {{ node.title }}
                                            </div>
                                        </q-btn> 
                                    </div>
                                    <q-separator></q-separator>
                                    <div v-if="node.type == 'Text'" class="q-pa-xs" style="min-width: 200px;">
                                        <div class="wrap rounded-1 q-pa-xs bg-grey-12" style="min-height: 80px;">
                                            {{ node.text }}
                                        </div>
                                    </div>
                                    <div v-if="node.type == 'Media'" class="q-pa-xs" style="min-width: 200px;">
                                        <div class="wrap rounded-1 q-pa-xs bg-grey-12 bg-grey-12 text-center full child">
                                            <q-img
                                                :src="node.src"
                                                style="max-height:75px; max-width: 100px;"
                                                class="rounded-1"
                                            />
                                        </div>
                                    </div>
                                    <div v-if="node.type == 'Frame'" class="q-pa-xs" style="min-width: 200px;">
                                        <div class="wrap rounded-1 q-pa-xs bg-grey-12 bg-grey-12 text-center full child">
                                            <iframe class="rounded-1 full-width" height="auto" 
                                                style="max-height: 75px; min-height: 70px; max-width: 100px;" 
                                                :src="node.src" 
                                                frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </q-scroll-area>
                </div>
            </div>
            <q-separator></q-separator>
            <!-- INTERACTION -->
            <!-- q-separator></q-separator-->
            <div class="font-8 row rounded-1 q-px-xs q-pt-xs full-width">
                <!-- q-separator vertical></q-separator-->
                <div class="col-2 col-md-3 full">
                    <q-btn-group glossy rounded dense spread class="q-pa-none grey-square inset-font">
                        <q-btn flat dense square size="xs" icon="share" class="inset-font q-pa-none" />
                        <q-btn flat dense square size="xs" icon="favorite" class="inset-font q-pa-none" />
                        <q-btn flat dense square size="xs" icon="bolt" class="inset-font q-pa-none" />
                    </q-btn-group>
                </div>
                <!-- Rate -->
                <div class="col-3 col-md-3 full q-pa-none text-center row">
                    <div class="col-6">
                        <q-btn flat dense spread :color="vote == 1 ? 'lime-13' : ''" size="xs" :label="rate.up" icon="thumb_up" 
                        class="q-px-xs text-dark-blue"
                        @click="rateUp()"
                        />
                    </div>
                    <div class="col-6">
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
                            :label="comments.length.toString() + ' comments'" 
                            :icon-right="expand_comments == true ? 'expand_less' : 'expand_more'" 
                            class="q-px-sm nasalization text-dark-blue text-right"
                            @click="expandComments()"
                        />
                    </div>
                    <!-- q-separator vertical></q-separator-->
                    <div class="col-6 text-right full-length q-px-xs q-pb-xs">
                        <q-btn push dense no-caps 
                            size="xs"
                            label="COMMENT" 
                            icon="add_comment" 
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
            <div class="full-width rounded-1 q-pa-xs">
                <!-- q-separator vertical></q-separator-->
                <div class="full-width row rounded-1">
                    <div class="col-9 col-md-10">
                        <span class="nasalization font-9 text-dark-blue q-px-xs q-pb-xs">Comments</span>
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
                <div v-for="(comment, c) in comments" :key="c" class="full-width q-pb-xs rounded-1">
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
  import CommentNester from 'src/components/PathCard/Actions/Nesters/CommentNester.vue'
  
  export default defineComponent({
    components: { CredentialTagScroll, CommentNester },
    name: 'BranchNester',
    data () {
        return {
            enabled_flag: this.enabled,
            pos_flag: this.pos,

            search_mode: true,
            show_references: false,
            word_style: "q-pa-none q-ml-xs disabled",
            sign_style: "q-pa-none disabled",

            // BRANCH STRUCTURE
            rate: { up: 3, down: 1 },
            vote: 0,
            date: ['3 days ago', 'Fri 31 Sep 2023 5:10:33'],
            branch_title: 'Please send weed',
            branch_nodes: [
                { type: 'Text', title: 'Cheetos Yellowness', text:'Cheeto yellowness depends on how much artificial colorant the cheetos have. The more orange, the more cheesy.' },
                { type: 'Frame', title: 'Cheetos - Chester Cheetah Commercial 1989', src:'https://www.youtube.com/embed/-dKPDkC9YqA?si=7Mgcmvfe8-SGnrmj' },
                { type: 'Media', title: 'An aberration', src:'https://user-images.githubusercontent.com/52062448/266973350-b9eaa6bc-f49a-4afa-92e8-4b893c171fb3.png' },
                { type: 'Text', title: 'Cheetos Yellowness', text:'Cheeto yellowness depends on how much artificial colorant the cheetos have. The more orange, the more cheesy.' }
            ],
            comments:[
                'comments/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                'comments/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'
            ],
            author: { 
                username: 'Allegue', 
                userpath: 'users/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                credentials: [
                    // { type: 'Profile', title: 'Twitter profile', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] },
                    { type: 'Community', title: 'Visual Artists', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] }
                    // { type: 'Organisation', title: 'UAEM', direction: 'https://twitter.com/ll3gu3', avatar: '', milestones: [ { title: 'Handball team student', direction: 'milestones/b93cbb7929' }, { title: 'High School diploma', direction: 'milestones/n73cbb7929'} ] }
                ]
            },
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
  