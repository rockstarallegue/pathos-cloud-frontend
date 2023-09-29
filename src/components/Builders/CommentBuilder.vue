<template>
    <q-card class="bg-gral hidden-oerflow text-white">
        <q-bar class="q-pt-sm bg-gral inset-font shadow-2 text-blue-grey nasalization hidden-overflow">
          <q-icon size="sm" name="speaker_notes" />
          <div class="font-6">Comment builder</div>

          <q-space />

          <q-btn dense flat icon="close" v-close-popup>
            <q-tooltip class="bg-white text-blue-grey">Close</q-tooltip>
          </q-btn>
        </q-bar>

        <q-card-section class="q-pa-sm">
          <div class="full container neon-surface grey-square text-center rounded-2" style="min-width: 500px; min-height: 300px;">
            <div class="full child light-2-glass q-pa-xs rounded-2 nasalization">

              <!-- BREADCRUMBS -->
              <div class="q-pa-xs q-gutter-sm text-dark-blue">
                <q-breadcrumbs>
                  <q-breadcrumbs-el icon="route" label="PATH" to="/" class="text-blue-grey"/>
                  <q-breadcrumbs-el label="Comments" icon="comment" to="/start/pick-quasar-flavour" class="text-blue-grey"/>
                  <q-breadcrumbs-el label="@mr_dreaminator" to="/vue-components/breadcrumbs" />
                </q-breadcrumbs>
              </div>

              <!-- SELECT & EDIT AUTHOR -->
              <div class="q-pa-xs q-gutter-sm">
                <div class="text-blue-grey grey-square shadow-1 text-left light-1-glass font-8 q-pa-xs rounded-2">
                  <q-icon name="face_5"></q-icon> Author's profile & credentials
                  <div class="full-width bg-grey-12 rounded-1 row q-pa-xs">
                    <!-- CHANGE AUTHOR -->
                    <div class="col-1 q-pa-none">
                      <q-btn flat dense size="md" icon="expand_more" class="full-width q-pa-none">
                        <q-menu>
                          <q-list style="min-width: 300px">
                            <q-item clickable v-close-popup>
                              <!-- AUTHOR -->
                              <div class="full-width row q-pa-xs">
                                <!-- avatar -->
                                <div class="col-1">
                                  <q-avatar rounded size="2em">
                                    <img :src="author.avatar">
                                  </q-avatar>
                                </div>
                                <!-- username -->
                                <div class="col-6">
                                  <div class="ellipsis q-px-xs text-left nasalization col">
                                      <div class="col-7 q-px-xs font-8">
                                        {{ author.username }}
                                      </div>
                                      <div class="col-5 q-px-xs font-7 text-grey">
                                        {{ author.userpath }}
                                      </div>
                                  </div>
                                </div>
                                <!-- credentials -->
                                <div class="col-5 q-px-sm">
                                  <CredentialTagScroll></CredentialTagScroll>
                                </div>
                              </div>
                            </q-item>
                          </q-list>
                        </q-menu>
                      </q-btn>
                    </div>
                    <!-- AUTHOR -->
                    <div class="col-7 row q-pa-xs">
                      <!-- avatar -->
                      <div class="col-1">
                        <q-avatar rounded size="2.2em">
                          <img :src="author.avatar">
                        </q-avatar>
                      </div>
                      <!-- username -->
                      <div class="col-5">
                        <div class="ellipsis q-px-xs text-left nasalization col">
                            <div class="col-7 q-px-xs font-8">
                              {{ author.username }}
                            </div>
                            <div class="col-5 q-px-xs font-7 text-grey">
                              {{ author.userpath }}
                            </div>
                        </div>
                      </div>
                      <!-- credentials -->
                      <div class="col-6 q-px-xs">
                        <CredentialTagScroll></CredentialTagScroll>
                      </div>
                    </div>
                    <!-- EDIT & ADD -->
                    <div class="col-4 row text-center">
                      <div class="col q-px-xs text-right">
                        <q-btn push dense no-caps 
                            size="md"
                            icon="edit"
                            icon-right="badge"
                            class="q-pa-none text-blue-grey q-pa-xs"
                        >
                          <q-tooltip class="bg-grey-12 text-blue-grey">
                              Edit credentials
                          </q-tooltip>
                        </q-btn>
                      </div>
                      <q-separator vertical></q-separator>
                      <div class="col-3 q-px-xs">
                        <q-btn push dense no-caps 
                            size="md"
                            icon="person_add"
                            class="q-pa-none text-blue-grey q-pa-xs"
                        >
                          <q-tooltip class="bg-grey-12 text-blue-grey">
                              Add profile
                          </q-tooltip>
                        </q-btn>
                      </div>
                      <q-separator vertical></q-separator>
                      <div class="col-3 q-px-xs">
                        <q-btn push dense no-caps 
                            size="md"
                            icon="supervised_user_circle"
                            class="q-pa-none text-blue-grey q-pa-xs"
                        >
                          <q-tooltip class="bg-grey-12 text-blue-grey">
                              Clone profile from this profile
                          </q-tooltip>
                        </q-btn>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
        
              <!-- SELECT REFERENCES -->
              <div class="q-pa-xs q-gutter-sm">
                <div class="text-blue-grey grey-square shadow-1 text-left light-1-glass font-8 q-pa-xs rounded-2">
                  <q-icon name="summarize"></q-icon> Add reference to reference list
                  <div class="row bg-grey-12 rounded-1">
                      <div class="col-3 q-pa-xs text-center row">
                        <q-select dense v-model="select_model" :options="options"
                            style="font-size: 12px;"
                            standout="bg-grey-13 text-blue-grey q-pa-none q-ma-none"
                            class="q-pa-none q-ma-none bg-grey-12 text-blue-grey rounded-1 nasalization">
                            <template v-slot:prepend>
                              <q-icon size="xs" :name="getIcon(select_model)" />
                            </template>
                        </q-select>
                      </div>
                      <div class="col-6 q-pa-xs rounded-1">
                          <q-select
                              dense
                              v-model="model"
                              use-input
                              size="xs"
                              input-debounce="0"
                              @new-value="createValue"
                              :options="filterOptions"
                              @filter="filterFn"
                              :label="select_model + '/'"
                              style="font-size: 12px;"
                              standout="bg-grey-13 text-blue-grey q-pa-none q-ma-none"
                              class="q-pa-none q-ma-none bg-grey-12 text-blue-grey rounded-1 nasalization"
                          >
                          </q-select>
                      </div>
                      <div class="col-3 q-pa-sm text-center row">
                        <!-- div class="col-3 q-pr-xs q-py-sm">
                          <q-btn flat outline icon="search" size="sm" class="bg-grey-12 q-pa-xs text-grey-blue "/>
                        </div-->
                        <div class="col-12">
                          <q-btn push icon="post_add" size="sm" label="Add to list" class="bg-grey-12 q-pa-sm text-grey-blue"/>
                        </div>
                      </div>
                  </div>
                </div>
              </div>

              <!-- WRITE COMMENT -->
              <div class="q-pa-xs q-gutter-sm">
                <div class="text-blue-grey grey-square shadow-1 text-left light-1-glass font-8 q-pa-xs rounded-2">
                  <q-icon name="edit_note"></q-icon> Write comment
                  <NoteBox></NoteBox>
                </div>
              </div>
              
              <!-- SEND -->
              <div class="q-pa-xs q-gutter-sm">
                <div class="font-8 q-pa-none rounded-1">
                  <div class="q-pa-none">
                    <q-btn push no-caps icon="comment" size="md" label="Publish comment" class="text-blue-grey bg-gral q-pa-xs full-width"/>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </q-card-section>
    </q-card>
</template>
  
  <script>
  import { defineComponent, ref } from 'vue'
  import NoteBox from 'src/components/Builders/Boxes/NoteBox.vue'
  import CredentialTagScroll from 'src/components/CredentialTagScroll.vue'

  const stringOptions = [
    'Google', 'Facebook', 'Twitter'
    ]
  
  export default defineComponent({
    components: { NoteBox, CredentialTagScroll },
    name: 'CommentBuilder',
    data () {
        return {
            show: this.bar,
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
    methods: {
      getIcon (model) {
        if(model == 'PATH') { return  'route'}
        if(model == 'NODE') { return  'adjust'}
        if(model == 'PROFILE') { return  'face_5'}
      },
    },
    setup () {
      const filterOptions = ref(stringOptions)

      return {
        select_model: ref('PATH'),

        options: [
          'PATH', 'NODE', 'PROFILE'
        ],
        model: ref(null),
        filterOptions,

        createValue (val, done) {
            // Calling done(var) when new-value-mode is not set or "add", or done(var, "add") adds "var" content to the model
            // and it resets the input textbox to empty string
            // ----
            // Calling done(var) when new-value-mode is "add-unique", or done(var, "add-unique") adds "var" content to the model
            // only if is not already set
            // and it resets the input textbox to empty string
            // ----
            // Calling done(var) when new-value-mode is "toggle", or done(var, "toggle") toggles the model with "var" content
            // (adds to model if not already in the model, removes from model if already has it)
            // and it resets the input textbox to empty string
            // ----
            // If "var" content is undefined/null, then it doesn't tampers with the model
            // and only resets the input textbox to empty string

            if (val.length > 0) {
            if (!stringOptions.includes(val)) {
                stringOptions.push(val)
            }
            done(val, 'toggle')
            }
        },

        filterFn (val, update) {
            update(() => {
            if (val === '') {
                filterOptions.value = stringOptions
            }
            else {
                const needle = val.toLowerCase()
                filterOptions.value = stringOptions.filter(
                v => v.toLowerCase().indexOf(needle) > -1
                )
            }
            })
        }
        }
    },
    props: {
        bar: {}
    }
    
  })
  </script>