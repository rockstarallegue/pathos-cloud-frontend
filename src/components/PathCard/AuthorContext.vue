<template>
    <div class="full-width row q-pa-none">
        <div class="q-pa-none q-px-sm full-width row">
            <!-- q-separator vertical></q-separator-->
            <div class="col q-px-none q-py-none">
                <q-btn dense flat no-caps align="left" class="font-8 q-pa-none q-px-xs text-black full-width nasalization">
                    <q-avatar rounded size="3em">
                      <img :src="author.avatar">
                    </q-avatar>
                    <div class="q-pa-none q-px-sm text-left col">
                        <div class="font-9 q-pt-xs">
                          {{ author.username }}
                          <div class="ellipsis font-9 text-grey-8">{{ author.userpath}}</div>
                        </div>
                        <!-- div class="col-6 bg-purple font-7 text-grey q-pa-none">
                          {{ author.userpath}}
                        </div-->
                    </div>
                    <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                        <div class="text-center text-black row">
                            <div class="q-pa-none text-center col-1">
                              <q-avatar rounded size="2em">
                                <img :src="author.avatar">
                              </q-avatar>
                            </div>
                            <div class="q-pa-xs text-left col-10">
                              {{ author.username }}
                            </div>
                        </div>
                        {{ author.userpath }}
                    </q-tooltip>
                </q-btn>
            </div>
            <!-- q-separator vertical></q-separator-->
            <div class="col-7 full child q-pa-xs">
              <div class="fit q-pa-none q-pa-xs light-1-glass rounded-2 grey-border-3">
                <CredentialTagScroll></CredentialTagScroll>
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
    name: 'AuthorContext',
    data () {
      return {
        author: { 
          username: 'Guandanarian',
          avatar:  'https://pbs.twimg.com/profile_images/1642271561347416064/tXvqo5nM_400x400.jpg',
          userpath: 'users/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
          credentials: [
              { type: 'Profile', title: 'Twitter profile', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] },
              { type: 'Community', title: 'Visual Artists', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [] },
              { type: 'Organisation', title: 'UAEM', direction: 'https://twitter.com/ll3gu3', avatar: '', milestones: [ { title: 'Handball team student', direction: 'milestones/b93cbb7929' }, { title: 'High School diploma', direction: 'milestones/n73cbb7929'} ] }
          ]
        }
      }
    },
    props: {
      author_prop: {
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
  