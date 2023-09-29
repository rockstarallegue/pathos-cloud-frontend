<template>
  <q-layout view="hHh lpR fFf" class="bg-grid">

    <q-drawer
        v-model="drawer"
        show-if-above

        :mini="!drawer || miniState"
        @click.capture="drawerClick"

        :width="200"
        :breakpoint="500"
        bordered
        :class="$q.dark.isActive ? 'bg-gral' : 'bg-gral' + ' shadow-1'"
      >
        <q-scroll-area class="fit" :horizontal-thumb-style="{ opacity: 0 }">
          <q-list class="nasalization inset-font">
            <q-item :active="$route.path === '/'" clickable @click="goRoute('/')" v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="route" />
              </q-item-section>

              <q-item-section>
                Path explorer
              </q-item-section>
            </q-item>

            <q-item :active="$route.path === '/node'" clickable @click="goRoute('/node')" v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="adjust" />
              </q-item-section>

              <q-item-section>
                Node explorer
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="label_important" />
              </q-item-section>

              <q-item-section>
                Label explorer
              </q-item-section>
            </q-item>

            <q-separator/>

            <q-item clickable v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="face_5" />
              </q-item-section>

              <q-item-section>
                Profiles
              </q-item-section>
            </q-item>

            <q-separator/>

            <q-item clickable v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="diversity_2" />
              </q-item-section>

              <q-item-section>
                Communities
              </q-item-section>
            </q-item>

            <q-item clickable v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="reduce_capacity" />
              </q-item-section>

              <q-item-section>
                Organisations
              </q-item-section>
            </q-item>

            <q-separator/>

            <q-item clickable v-ripple active-class="my-menu-link">
              <q-item-section avatar>
                <q-icon name="shopping_basket" />
              </q-item-section>

              <q-item-section>
                Hypermarket
              </q-item-section>
            </q-item>
            
            <q-separator/>
          </q-list>
        </q-scroll-area>

        <!--
          in this case, we use a button (can be anything)
          so that user can switch back
          to mini-mode
        -->
        <div class="q-mini-drawer-hide absolute" style="top: 15px; right: -17px">
          <q-btn
            dense
            round
            unelevated
            color="grey"
            icon="chevron_left"
            @click="miniState = true"
          />
        </div>
      </q-drawer>

    <q-page-container>
      <router-view @pin="(pin) => pinElement(pin)"/>
    </q-page-container>

    <q-footer bordered class="bg-gral q-pa-none text-grey shadow-1">
      <q-toolbar>
          <q-btn flat @click="drawer = !drawer" round dense icon="menu" class="inset-font"/>
          <q-toolbar-title v-if="$q.platform.is.desktop" class="nasalization inset-font text-grey"><span class="text-dark-blue">Path explorer</span></q-toolbar-title>
          <q-space></q-space>
          <!-- div class="nasalization inset-font row" -->
            <!-- <- -->
            <!-- <div class="neon-aqua rounded-2">
              <q-btn dense push :size="$q.platform.is.desktop ? 'md' : 'sm' " class="light-2-glass text-dark-blue q-pa-none q-mr-xs">
                <div class="bg-grey-12 rounded-1 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.2em" name="arrow_back" class="inset-font"></q-icon>
                </div>
              </q-btn>
            </div>
            <q-btn dense push :size="$q.platform.is.desktop ? 'md' : 'sm' " icon="arrow_back_ios" icon-right="flag" class="light-2-glass text-dark-blue q-mr-xs q-px-sm"/>
            <q-btn push rounded :size="$q.platform.is.desktop ? 'lg' : 'md' " dense icon="flag_circle" class="text-dark-blue neon-candy-btn q-pa-xs q-mr-xs"/>
            <q-btn dense push :size="$q.platform.is.desktop ? 'md' : 'sm' " icon="flag" icon-right="arrow_forward_ios" class="light-2-glass text-dark-blue q-mr-xs q-px-sm"/>
            <q-btn dense push :size="$q.platform.is.desktop ? 'md' : 'sm' " icon="arrow_forward" class="light-2-glass text-dark-blue q-pa-xs q-mr-xs"/>
          </div>
          <q-space></q-space-->
          
          <!-- <- -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="arrow_back" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint <- -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="arrow_back_ios" class="inset-font"></q-icon>
                  <q-icon size="1.5em" name="flag" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint -->
          <div class="neon-candy-cake q-pa-none q-mx-xs" style="border-radius: 10em;">
            <q-btn push dense rounded size="md"
              class="rounded-2 q-pa-none q-pb-xs text-blue-grey" style="border-radius: 10em;">
                <div class="light-2-glass rounded-2 nasalization q-pa-none" style="border-radius: 10em;">
                  <q-icon size="2.8em" name="flag_circle" class="text-dark-blue"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint -> -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="flag" class="inset-font"></q-icon>
                  <q-icon size="1.5em" name="arrow_forward_ios" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- -> -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="arrow_forward" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <q-space></q-space>
          <!-- PIN -->
          <div class="neon-cake rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-1 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.2em" name="push_pin" class="inset-font"></q-icon>
                  <span v-if="$q.platform.is.desktop" class="font-10 q-px-xs">Pinned</span>
                </div>
              <q-badge rounded class="nasalization text-dark-blue neon-cake shadow-1 grey-square" floating>{{ pinned_elements.length }}</q-badge>
              <q-menu
                transition-show="scale"
                transition-hide="scale"
                class="bg-gral q-pa-sm rounded-2"
              >
                <div class="q-pa-xs nasalization inset-font text-blue-grey bg-gral row">
                    <div class="col-11">Pinned elements</div>
                    <div class="col-1 text-right">
                      <q-btn
                            flat dense style="color: #404258;" size="sm" icon="search" 
                            class="nasalization full-width inset-font q-pa-none text-blue-grey"
                        />
                    </div>
                </div>
                <q-list style="max-width: 25em" class="q-pa-none neon-cake rounded-2">
                  <div class="q-pa-xs light-2-glass grey-square rounded-2">
                    <q-item v-for="(pinned, n) in pinned_elements" 
                      :key="n" 
                      clickable
                      class="bg-grey-12 nasalization q-pa-xs grey-square q-ma-xs rounded-2">
                      <q-item-section class="q-pa-none">
                        <div class="ellipsis full-width font-8 text-blue-grey q-px-sm">
                          <div class="font-8 text-grey-6 q-pa-none full-width">
                            <q-icon size="1em" name="push_pin"></q-icon>
                            08:24 PM
                          </div>
                        </div>
                        <div class="ellipsis full-width font-8 text-blue-grey q-px-sm">
                          <q-icon :name="pinIcon(pinned.type)" size="1.2em"></q-icon>
                          :: {{ pinned.title }} :: <span class="text-grey-8">{{ pinned.direction }}</span>
                        </div>
                      </q-item-section>
                      <q-item-section vertical class="q-pa-none text-left" style="max-width: 30px">
                        <q-btn push rounded size="sm" icon="file_copy" color="blue-13" class="q-pa-none"></q-btn>
                      </q-item-section>
                      <q-item-section vertical class="q-pa-none q-mr-sm text-left" style="max-width: 30px">
                        <q-btn push rounded size="sm" icon="cancel" color="red-13" class="q-pa-none"></q-btn>
                      </q-item-section>
                    </q-item>
                  </div>
                </q-list>
              </q-menu>
            </q-btn>
          </div>
          <!-- NOTES -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-1 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.2em" name="developer_board" class="inset-font"></q-icon>
                  <span v-if="$q.platform.is.desktop" class="font-10 q-px-xs">Notes</span>
                </div>
              <q-badge rounded class="neon-aqua text-dark-blue nasalization shadow-1 grey-square" floating>{{ pinned_elements.length }}</q-badge>
              <q-menu
                transition-show="scale"
                transition-hide="scale"
                class="bg-gral q-pa-sm rounded-2"
                style="min-width: 45em" 
              >
                <div class="q-pa-xs nasalization inset-font text-blue-grey bg-gral row">
                    <div class="col-11">Notes</div>
                    <div class="col-1 text-right">
                      <q-btn
                            flat dense style="color: #404258;" size="sm" icon="search" 
                            class="nasalization full-width inset-font q-pa-none text-blue-grey"
                        />
                    </div>
                </div>
                <div class="q-pa-none fit neon-aqua grey-square rounded-2">
                  <NotePad></NotePad>
                </div>
              </q-menu>
            </q-btn>
          </div>
          <!-- BUILDER -->
          <div class="neon-surface rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              @click="bar2 = true"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-1 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.2em" name="rebase_edit" class="inset-font"></q-icon>
                  <span v-if="$q.platform.is.desktop" class="font-10 q-px-xs">Building</span>
                </div>
              <div class="full-width">
                <q-badge dense class="nasalization text-dark-blue neon-surface shadow-1 q-mb-xl grey-square font-7 badge-padding" floating>
                  <q-icon size="1em" name="comment"/>{{ pinned_elements.length }}
                </q-badge>
                <q-badge dense class="nasalization text-dark-blue neon-surface shadow-1 q-mr-lg q-mb-xl grey-square font-7 badge-padding" floating>
                  <q-icon size="1em" name="adjust" />{{ pinned_elements.length }}
                </q-badge>
                <q-badge dense class="nasalization text-dark-blue neon-surface shadow-1 q-mr-xl q-mb-xl grey-square font-7 badge-padding" floating>
                  <q-icon size="1em" name="route"/>{{ pinned_elements.length }}
                </q-badge>
              </div>
              
            </q-btn>
          </div>
        </q-toolbar>
    </q-footer>

    <q-dialog v-model="bar2" transition-show="flip-down" transition-hide="flip-up">
      <CommentBuilder :bar="'daunfdsfnd'"></CommentBuilder>
    </q-dialog>
    

  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import CommentBuilder from 'src/components/Builders/CommentBuilder.vue'
import NotePad from 'src/components/NotePad.vue'

export default defineComponent({
  components: { CommentBuilder, NotePad },
  name: 'MainLayout',
  data () {
    return {
      pinned_elements: [
        { type: 'Node', title: 'YC', direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Profile', title: 'Mr. Dreaminator', direction: 'profile/f76576cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Path', title: 'Cool stuff', direction: 'paths/f40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'}
      ]
    }
  },
  methods: {
    goRoute (route) {
      (this.$route.path === route) ? location.reload() : this.$router.push(route)
    },
    pinElement(e){
      // Calling API if not pinned
      this.pinned_elements.push(e)
      console.log(this.pinned.toString())
    },
    pinIcon (type) {
      if(type == 'Path') { return 'route'; }
      if(type == 'Tag') { return 'label_important'; }
      if(type == 'Profile') { return 'face_5'; }
      if(type == 'Community') { return 'diversity_2'; }
      if(type == 'Organisation') { return 'reduce_capacity'; }
      if(type == 'Hypermarket') { return 'shopping_basket'; }
      else { return 'adjust'; }
  }
  },
  setup () {
    const miniState = ref(false)

    return {
      bar2: ref(false),
      drawer: ref(false),
      miniState,

      drawerClick (e) {
        // router.push({ path: 'node' })
        console.log("click: ", e)
        // (this.$route.path === "/node") ? location.reload() : this.$router.push("/node")
        // if in "mini" state and user
        // click on drawer, we switch it to "normal" mode
        if (miniState.value) {
          miniState.value = false

          // notice we have registered an event with capture flag;
          // we need to stop further propagation as this click is
          // intended for switching drawer to "normal" mode only
          e.stopPropagation()
        }
      }
    }
  }
})
</script>
