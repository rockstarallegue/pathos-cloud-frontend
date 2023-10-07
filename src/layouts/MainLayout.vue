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
          <q-list>
            <NavigationMap :drawer_flag="miniState" :steps="steps"></NavigationMap>
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
          <!-- <- -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
            @click="mapStep('backward', 'the direction')"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="arrow_back" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint bck <- -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
              @click="mapStep('backward_checkpoint', 'the direction')"
              class="rounded-2 q-pa-none q-px-none q-pb-xs text-blue-grey">
                <div class="bg-grey-12 rounded-2 grey-borders q-pa-xs q-px-sm nasalization inset-font">
                  <q-icon size="1.5em" name="arrow_back_ios" class="inset-font"></q-icon>
                  <q-icon size="1.5em" name="flag" class="inset-font"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint -->
          <div class="neon-candy-cake q-pa-none q-mx-xs" 
            @click="mapStep('checkpoint', 'the direction')" style="border-radius: 10em;">
            <q-btn push dense rounded size="md"
              class="rounded-2 q-pa-none q-pb-xs text-blue-grey" style="border-radius: 10em;">
                <div class="light-2-glass rounded-2 nasalization q-pa-none" style="border-radius: 10em;">
                  <q-icon size="2.8em" name="flag_circle" class="text-dark-blue"></q-icon>
                </div>
            </q-btn>
          </div>
          <!-- checkpoint fwd -> -->
          <div class="neon-aqua rounded-2 q-mx-xs">
            <q-btn push dense square size="md"
            @click="mapStep('forward_checkpoint', 'the direction')"
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
              @click="mapStep('forward_checkpoint', 'the direction')"
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
                  <!-- span v-if="$q.platform.is.desktop" class="font-10 q-px-xs">Pinned</span-->
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
                class="bg-gral q-pa-none rounded-2 grey-square"
                style="max-width: 40em; max-height: 40em;" 
              >
                <div class="q-pa-none full-width nasalization bg-gral text-blue-grey row rounded-2">
                  <q-bar class="full-width q-px-none bg-gral shadow-1 q-pa-xs rounded-u-1">
                    <!--q-btn dense flat round icon="lens" size="8.5px" color="red" /-->
                    <q-btn dense flat round icon="lens" size="8.5px" color="yellow" />
                    <q-btn dense flat round icon="lens" size="8.5px" color="green" />
                    <q-space />
                    <q-btn dense flat icon="developer_board" />
                    <div class="text-weight-bold">
                      NOTEPAD
                    </div>
                    <q-space />
                    <q-btn dense flat icon="search" />
                    <q-btn dense flat icon="restore_from_trash" />
                  </q-bar>
                </div>
                <div class="q-pa-none full child fit bg-gral">
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
import NavigationMap from 'src/components/NavigationMap.vue'

export default defineComponent({
  components: { CommentBuilder, NotePad, NavigationMap },
  name: 'MainLayout',
  data () {
    return {
      // the_drawer_flag: drawer_flag,
      pinned_elements: [
        { type: 'Node', title: 'YC', direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Profile', title: 'Mr. Dreaminator', direction: 'profile/f76576cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Path', title: 'Cool stuff', direction: 'paths/f40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
        { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'}
      ],
      // steps node
      steps: [
        {
        label: 'PathosCloud',
        header: 'root',
        icon: 'adjust',
        type: 'move',
        move: 'login',
        direction: 'moments/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        time: '07:34 PM',
        children:
        [
            { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
            { header: 'generic', label: 'Shared', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
        ]
        },
        {
        label: 'Allegue',
        header: 'root',
        icon: 'face_5',
        type: 'checkpoint',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        children: [
            {
            label: 'My Type',
            header: 'root',
            icon: 'adjust',
            type: 'move',
            move: 'forward',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children:
            [
                { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                { header: 'generic', label: 'Share', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
            ]
            },
            {
            label: 'Allegue',
            header: 'root',
            icon: 'face_5',
            type: 'checkpoint',
            move: 'checkpoint',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children: [
                {
                label: 'My Type',
                header: 'root',
                icon: 'adjust',
                type: 'move',
                move: 'forward_checkpoint',
                direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                children:
                [
                    { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                    { header: 'generic', label: 'Share', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
                ]
                },
                {
                label: 'Old Soul',
                header: 'root',
                icon: 'adjust',
                type: 'move',
                move: 'backward_checkpoint',
                direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                children:
                [
                    { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                    { header: 'generic', abel: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
                ]
                },
            ]
            },
            {
            label: 'Old Soul',
            header: 'root',
            icon: 'adjust',
            type: 'move',
            move: 'click',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children:
            [
                { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                { header: 'generic', abel: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
            ]
            },
        ]
        },
        {
        label: 'Y Combinator',
        header: 'root',
        icon: 'route',
        type: 'move',
        move: 'backward',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        time: '07:34 PM',
        children:
        [
            { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
            { header: 'generic', label: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
        ]
        },
        {
        label: 'Saint Motel',
        header: 'root',
        icon: 'diversity_2',
        type: 'move',
        move: 'forward',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        children:
        [
            { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
            { header: 'generic', label: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
        ]
        },
        {
        label: 'My Type',
        header: 'root',
        icon: 'adjust',
        type: 'move',
        move: 'forward',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        children:
        [
            { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
            { header: 'generic', label: 'Share', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
        ]
        },
        {
        label: 'Old Soul',
        header: 'root',
        icon: 'adjust',
        type: 'move',
        move: 'click',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        children:
        [
            { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
            { header: 'generic', abel: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
        ]
        },
        {
        label: 'Allegue',
        header: 'root',
        icon: 'face_5',
        type: 'checkpoint',
        direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        children: [
            {
            label: 'My Type',
            header: 'root',
            icon: 'adjust',
            type: 'move',
            move: 'forward',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children:
            [
                { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                { header: 'generic', label: 'Share', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
            ]
            },
            {
            label: 'Allegue',
            header: 'root',
            icon: 'face_5',
            type: 'checkpoint',
            move: 'checkpoint',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children: [
                {
                label: 'My Type',
                header: 'root',
                icon: 'adjust',
                type: 'move',
                move: 'forward_checkpoint',
                direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                children:
                [
                    { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                    { header: 'generic', label: 'Share', type: 'action', icon: 'share', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
                ]
                },
                {
                label: 'Old Soul',
                header: 'root',
                icon: 'adjust',
                type: 'move',
                move: 'backward_checkpoint',
                direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
                children:
                [
                    { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                    { header: 'generic', abel: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
                ]
                },
            ]
            },
            {
            label: 'Old Soul',
            header: 'root',
            icon: 'adjust',
            type: 'move',
            move: 'click',
            direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
            children:
            [
                { header: 'generic', label: 'Marked as favorite', type: 'action', icon: 'favorite', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' },
                { header: 'generic', abel: 'Commented', type: 'action', icon: 'chat', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173' }
            ]
            },
        ]
        }
      ],
      checkpoint_stack: [],
      step_stack: [] // We can put checkpoint stacks inside the checkpoint stack
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
    },
    mapStep(action, direction){
      var stype = action == 'checkpoint' ? 'checkpoint' : 'move';
      // if(this.steps[0].type == )
      var map_step = {
        label: 'New Step',
        header: 'root',
        icon: 'adjust',
        type: stype,
        move: action,
        direction: 'node/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173',
        time: '07:34 PM'
      }
      this.steps.unshift(map_step)
    }
  },
  setup () {
    const miniState = ref(false)
    // const drawer_flag = false

    return {
      bar2: ref(false),
      drawer: ref(false),
      miniState,
      // drawer_flag,

      drawerClick (e) {
        // drawer_flag = drawer_flag == false ? true : false;
        console.log('DRAWER: ', miniState.value)
        // router.push({ path: 'node' })
        // console.log("drawer clicked: ", this.drawer)
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
      },

    }
  }
})
</script>
