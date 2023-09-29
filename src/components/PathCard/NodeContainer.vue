<template>
    <div class="q-pa-none q-mt-xs q-mb-sm rounded-1 container child">
      <q-card flat bordered class="q-pa-none light-1-glass-2">
        <q-card-section class="q-pa-none rounded-u-1">
          <!-- INFO BUTTONS -->
          <div class="full-width q-pa-none row">
              <div class="col-1 text-center q-py-xs">
                <q-btn
                  rounded size="sm" icon="adjust" 
                  class="nasalization bg-grey-11 inset-font q-px-xs"
                >
                    <q-tooltip class="bg-grey-13 text-black font-11 text-center nasalization inset-font">
                        {{ node_buffer }}
                        <div class="q-pa-xs font-9 text-black row">
                            <div class="col text-center">
                                <q-icon size="1.2em" name="face_5" class="q-pa-none"></q-icon>
                                :: {{ author.username }}
                            </div>
                            <div class="ellipsis text-dark-blue col-8 q-px-xs">
                                ({{ author.userpath }})
                            </div>
                            <div class="col text-left">
                                [{{ date[0] }}]
                            </div>
                        </div>
                    </q-tooltip>
                </q-btn>
              </div>
              <q-separator vertical></q-separator>
              <div class="col-5 col-md-6 text-left text-title q-pa-xs">
                <q-btn flat no-caps size="0.8em" class="bg-grey-12 text-dark-blue nasalization full-width">
                  <div class="ellipsis q-pa-none q-px-xs font-12">
                    <q-icon size="1.2em" :name="getTypeIcon(node_type)" class="q-pa-none"></q-icon> :: {{ title_name }}
                  </div>
                </q-btn>  
              </div>
              <q-separator vertical></q-separator>
              <!-- WORD BUTTON -->
              <div class="col row">
                <div class="col text-center q-pa-xs">
                  <q-btn
                    flat dense style="color: #404258;" size="sm" icon="location_searching" 
                    class="full-width inset-font"
                    @click="switchToSearchMode()"
                  />
                </div>
                <!-- q-separator vertical></q-separator>
                <div class="col text-center q-pa-xs">
                  <q-btn
                    flat dense style="color: #404258;" size="sm" icon="content_paste"
                    class="full-width inset-font"
                    @click="copyPath()"
                  />
                </div-->
                <q-separator vertical></q-separator>
                <div class="col text-center q-pa-xs">
                  <q-btn
                        flat dense style="color: #404258;" size="sm" icon="summarize"
                        class="full-width inset-font"
                        @click="showAllReferences()"
                  >
                    <q-badge color="grey-12" class="text-dark-blue nasalization q-pa-none q-px-xs" floating>{{ node_references.length }}</q-badge>
                  </q-btn>
                </div>
              </div>
              <q-separator vertical></q-separator>
                <div class="col-1 text-center q-pa-xs">
                    <q-btn push dense no-caps 
                        size="xs"
                        icon="push_pin"
                        class="q-pa-xs text-grey-12 bg-pink-13"
                    />
                </div>
              <q-separator vertical></q-separator>
              <!-- MORE DROPDOWN BUTTON -->
              <div class="col-2 col-md-1 text-center q-pa-xs">
                  <q-btn-dropdown 
                      dense flat style="color: #404258;" size="xs" icon="more_vert"
                      class="nasalization q-px-xs inset-font"  
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
  
          <q-separator></q-separator>
  
            <!-- TEXT -->
            <div v-if="node_type === 'text'" class="full-width q-pa-none row">
                <div class="fit q-pa-xs">
                    <!-- q-separator vertical></q-separator-->
                    <div class="flex justify-around bg-grey-12 q-pa-none rounded-2">
                        <!-- q-separator vertical></q-separator-->
                        <div v-if="search_mode === true" class="flex justify-around rounded-2 q-pa-xs">
                            <q-btn
                                v-for="(word_obj, n) in node_text" 
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
                                v-for="(word_obj, n) in node_text" 
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

            <!-- MEDIA -->
            <div v-if="node_type === 'media'" class="full-width q-pa-none row">
                <div class="flex flex-center q-pa-xs full">
                    <div class="q-pa-sm rounded-2 bg-grey-12 text-center full child">
                        <q-img
                            src="~assets/gif-3.gif"
                            style="max-height:352px; max-width: 380px;"
                            class="rounded-1"
                        />
                    </div>
                </div>
            </div>

            <!-- FRAME -->
            <div v-if="node_type === 'frame'" class="full-width q-pa-none row">
                <div class="q-pa-xs full-width">
                    <div class="bg-grey-12 q-pa-sm rounded-1 flex items-center">
                        <iframe class="rounded-1 full-width" height="auto" style="max-height: 700px; min-height: 352px;" :src="node_text" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
                    </div>
                </div>
            </div>


            <q-separator></q-separator>
          
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
                                    <span class="nasalization font-9 inset-font text-dark-blue q-px-xs q-pb-xs">References</span>
                                </div>
                                <div class="col full-width text-right row">
                                     <!-- sort -->
                                    <div class="q-pa-none col">
                                        <q-btn-dropdown 
                                            dense
                                            flat
                                            size="xs"
                                            icon="sort"
                                            class="q-px-xs text-dark-blue inset-font"  
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
                                            class="q-px-xs text-dark-blue inset-font"  
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
                                v-for="(reference, r) in node_references" 
                                class="full-width nasalization" :key="r"
                            >
                            <div v-if="reference.enabled == true" class="full-width q-py-xs">
                                <q-btn no-caps rounded dense align="left" :icon="referenceIcon(reference.type)"
                                    class="font-8 q-px-xs text-dark-blue full-width bg-grey-12">
                                    <div class="ellipsis q-px-xs text-grey-8">
                                        {{ reference.author }} - <span class="text-dark-blue">{{ reference.title }}</span>
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
        </q-card-section>
      </q-card>
    </div>
  </template>
  
  <script>
  import { defineComponent } from 'vue'
  
  export default defineComponent({
    name: 'NodeContainer',
    data () {
      return {
        show_references: false,
        search_mode: true,
        word_style: "q-pa-none q-ml-xs disabled",
        sign_style: "q-pa-none disabled",
        // word_array: ['Lorem', 'ipsum', 'dolor', 'sit', 'amet', ',', 'consectetur', 'adipisicing', 'elit', ',', 'sed', 'do', 'eiusmod', 'tempor', 'incididunt', 'ut', 'labore', 'et', 'dolore', 'magna', 'aliqua.', 'Lorem', 'ipsum', 'dolor', 'sit', 'amet', ',', 'consectetur', 'adipisicing', 'elit', ',', 'sed', 'do', 'eiusmod', 'tempor', 'incididunt', 'ut', 'labore', 'et', 'dolore', 'magna', 'aliqua', '.']
        words_array: [
          { word: 'Lorem', tags: ['word', 'plain'] }, { word: 'ipsum', tags: ['word', 'plain'] }, { word: 'dolor', tags: ['word', 'plain'] }, { word: 'sit', tags: ['word', 'plain'] }, { word: 'amet', tags: ['word', 'plain'] }, { word: ',', tags: ['sign', 'plain'] }, { word: 'consectetur', tags: ['word', 'plain'] }, { word: 'adipisicing', tags: ['word', 'plain'] }, { word: 'elit', tags: ['word', 'plain'] }, { word: ',', tags: ['sign', 'plain'] }, { word: 'sed', tags: ['word', 'plain'] }, { word: 'do', tags: ['word', 'plain'] }, { word: 'eiusmod', tags: ['word', 'plain'] }, { word: 'tempor', tags: ['word', 'plain'] }, { word: 'incididunt', tags: ['word', 'plain'] }, { word: 'ut', tags: ['word', 'plain'] }, { word: 'labore', tags: ['word', 'plain'] }, { word: 'et', tags: ['word', 'plain'] }, { word: 'dolore', tags: ['word', 'plain'] }, { word: 'magna', tags: ['word', 'plain'] }, { word: 'aliqua', tags: ['word', 'plain'] }, { word: 'Lorem', tags: ['word', 'plain'] }, { word: 'ipsum', tags: ['word', 'plain'] }, { word: 'dolor', tags: ['word', 'plain'] }, { word: 'sit', tags: ['word', 'plain'] }, { word: 'amet', tags: ['word', 'plain'] }, { word: ',', tags: ['sign', 'plain'] }, { word: 'consectetur', tags: ['word', 'plain'] }, { word: 'adipisicing', tags: ['word', 'plain'] }, { word: 'elit', tags: ['word', 'plain'] }, { word: ',', tags: ['sign', 'plain'] }, { word: 'sed', tags: ['word', 'plain'] }, { word: 'do', tags: ['word', 'plain'] }, { word: 'eiusmod', tags: ['word', 'plain'] }, { word: 'tempor', tags: ['word', 'plain'] }, { word: 'incididunt', tags: ['word', 'plain'] }, { word: 'ut', tags: ['word', 'plain'] }, { word: 'labore', tags: ['word', 'plain'] }, { word: 'et', tags: ['word', 'plain'] }, { word: 'dolore', tags: ['word', 'plain'] }, { word: 'magna', tags: ['word', 'plain'] }, { word: 'aliqua', tags: ['word', 'plain'] }, { word: '.', tags: ['sign', 'plain'] }
        ],
        title_name: "Lorem ipsum",
        node_buffer: "nodes/ad6ee3e45a3bfa450d7de201cd354f90a17651e06c1d4b8e9b2b76ae1330c735",

        date: ['3 days ago', 'Fri 31 Sep 2023 5:10:33'],
        author: { 
          username: 'Guandanarian',
          userpath: 'profiles/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        },
        node_references: this.prop_node_references,
        node_text: this.prop_node_content
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
          this.word_style = "q-px-xs q-ml-xs q-mt-xs light-1-glass text-grey-11 nasalization borders-1"
        }
      },
      copyPath () {
        this.$refs.myinput.focus();
        document.execCommand('copy');
      },
      getTypeIcon (t) {
        if(t == 'text') { return 'article';}
        if(t == 'media') { return 'perm_media';}
        if(t == 'frame') { return 'language';}
        else { return 'link'}
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
            for(let i=0; i<this.node_references.length; i++){
                this.node_references[i].enabled = false;
            }
            for(let i=0; i<refs.length; i++){
                this.node_references[refs[i]].enabled = true;
            }
            
        },
        showAllReferences () {
            this.show_references = this.show_references == true ? false : true;
            for(let i=0; i<this.node_references.length; i++){
                this.node_references[i].enabled = true;
            }
        },
        hideReferences () {
            this.show_references = false;
            for(let i=0; i<this.node_references.length; i++){
                this.node_references[i].enabled = false;
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
        }
    },
    props: {
        node_type: {},
        prop_node_content: {},
        prop_node_references: {}
    }
  })
  </script>
  