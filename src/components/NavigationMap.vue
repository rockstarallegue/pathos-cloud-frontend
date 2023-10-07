<template>
    <div class="bg-gral q-pa-xs">
        <div class="text-grey-6 nasalization font-8 q-pa-none q-py-xs text-center">
            <q-icon size="1.5em" name="map" class="q-pr-xs text-dark-blue inset-font"/><span v-if="drawer_flag == false" class="text-dark-blue">NAVIGATION MAP</span>
        </div>
        <div class="q-pa-none neon-surface rounded-2">
            <div class="full-width q-pa-none q-py-xs light-2-glass rounded-2 grey-square-2">
                <q-scroll-area style="height: 19.4em;" class="q-pa-none">
                    <div class="q-pa-none nasalization">
                        <q-tree
                        :nodes="steps"
                        dense
                        node-key="label"
                        v-model:expanded="expanded"
                        class="text-grey-6 font-6 rounded-2 q-pa-none"
                        >
                            <template v-slot:header-root="prop">
                                <div class="row fit q-pa-none">
                                    <div class="fit">
                                        <q-badge v-if="drawer_flag == false" class="q-pa-none transparent text-grey-6 q-px-xs q-mt-sm font-9">
                                            <q-icon v-if="prop.node.move == 'backward_checkpoint' || prop.node.move == 'forward_checkpoint' " size="1.2em" name="flag"/>
                                            <q-icon size="1.2em" class="q-mx-xs" :name="getMoveIcon(prop.node.move)"/>
                                            08:45:43 PM
                                        </q-badge>
                                        <!-- CHECKPOINT ROOT -->
                                        <q-btn push v-if="prop.node.type == 'checkpoint'" rounded size="1em" class="q-pa-none q-pb-xs q-ml-xs nasalization neon-surface grey-square text-blue-grey">
                                            <div v-if="drawer_flag == true" class="ellipsis q-pa-none bg-grey-12 rounded-3 grey-borders"><q-icon size="2.2em" name="flag_circle"/></div>
                                            <div v-if="drawer_flag == false" class="ellipsis q-pa-xs bg-grey-12 rounded-3 grey-borders" style="max-width: 18.6em;">
                                                <q-icon v-if="drawer_flag == false" size="1.2em" name="flag_circle"/>
                                                ::
                                                <q-icon v-if="drawer_flag == false" size="1.2em" :name="prop.node.icon"/>
                                                :: {{ prop.node.label }} ::
                                                <span class="text-grey-6"> {{ prop.node.direction }} </span>
                                            </div>
                                        </q-btn>
                                        <!-- NORMAL ROOT -->
                                        <q-btn v-if="prop.node.type != 'checkpoint'" rounded size="1em" class="q-pa-none q-px-xs q-ml-xs nasalization bg-grey-12 grey-square text-blue-grey">
                                            <q-icon size="1.2em" :name="prop.node.icon"/>
                                            <div v-if="drawer_flag == false" class="ellipsis q-px-xs" style="max-width: 16.4em;">
                                                :: {{ prop.node.label }} ::
                                                <span class="text-grey-6"> {{ prop.node.direction }} </span>
                                            </div>
                                        </q-btn>
                                    </div>
                                </div>
                            </template>

                            <template v-slot:header-generic="prop">
                                <div class="full-width q-pr-xs">
                                    <div class="fit">
                                        <q-btn flat size="0.9em" class="q-pa-none q-px-xs q-ml-xs nasalization text-blue-grey">
                                            <div v-if="drawer_flag == false" class="ellipsis q-px-xs" style="max-width: 16.4em;">
                                                <q-icon size="1.2em" :name="prop.node.icon"/> :: 
                                                <span class="text-grey-6"> {{ prop.node.direction }} </span>
                                            </div>
                                        </q-btn>
                                    </div>
                                    <!-- q-badge color="orange" class="q-ml-sm">New!</q-badge-->
                                </div>
                            </template>
                        </q-tree>
                    </div>
                </q-scroll-area>
            </div>
        </div>

        <div class="text-grey-6 nasalization font-8 q-pa-none q-py-xs q-pt-sm text-center">
            <q-icon size="1.5em" name="keyboard" class="q-pr-xs text-dark-blue"/><span v-if="drawer_flag == false" class="text-dark-blue">KEY HEAT MAP</span>
        </div>
        <div class="q-px-none neon-surface rounded-2">
            <div class="full-width light-2-glass q-px-xs rounded-2 grey-square-2">
                <q-scroll-area style="height: 1.7em; max-width: 300px;">
                    <div class="row no-wrap">
                        <div v-for="(key, k) in moves" :key="k" class="q-pa-none">
                            <div class="col">
                                <div class="col">
                                    <q-btn dense size="xs" class="nasalization text-grey-12 q-pa-none q-px-xs q-mr-xs" :label="key.key" :style="'background-color: rgba(' + ((((maxi - mini) / key.diff) * 42/100 ) + 96) + ', 139, 96, 0.66);'">
                                    </q-btn>
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
  import { defineComponent, ref } from 'vue'

  var the_note = ''
  export default defineComponent({
    name: 'NavigationMap',

    data() {
        return {
            // the_note: ''
            //this_note: this.prop_note
            moves: [],
            maxi: -1,
            mini: 100000,
            visited_elements: [
                { type: 'Node', title: 'YC', direction: 'nodes/c40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
                { type: 'Profile', title: 'Mr. Dreaminator', direction: 'profile/f76576cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
                { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
                { type: 'Path', title: 'Cool stuff', direction: 'paths/f40976cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'},
                { type: 'Community', title: 'Cool stuff', direction: 'community/a30986cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173'}
            ]
        }
    },
    setup () {
      return {
            text: ref(''),
            title: ref(''),
            note: ref(the_note),
            expanded: ref([ 'Satisfied customers (with avatar)', 'Good food (with icon)' ]),

            simple_2: [
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
            ]
        }
    },
    created() {
        window.addEventListener('keydown', (e) => {
            const d = new Date();
            const t = d.getTime();
            // console.log('['+ t +'] '+"PRESSING: ", e.key);
            let keypress = {time:t, key:e.key, diff:t - this.moves[0].time};

            this.mini = Math.min(this.mini, keypress.diff)
            this.maxi = Math.max(this.maxi, keypress.diff)

            this.moves.unshift(keypress)
        });
    },
    methods: {
        initMoves () {
            const d = new Date();
            const t = d.getTime();
            let keypress = {time:t, key:'', diff:0};
            this.moves.push(keypress)
        },
        getIcon (type) {
            if(type == 'Path') { return 'route'; }
            if(type == 'Tag') { return 'label_important'; }
            if(type == 'Profile') { return 'face_5'; }
            if(type == 'Community') { return 'diversity_2'; }
            if(type == 'Organisation') { return 'reduce_capacity'; }
            if(type == 'Hypermarket') { return 'shopping_basket'; }
            else { return 'adjust'; }   
        },
        getMoveIcon (type) {
            if(type == 'backward') { return 'arrow_back'; }
            if(type == 'forward') { return 'arrow_forward'; }
            if(type == 'backward_checkpoint') { return 'first_page'; }
            if(type == 'forward_checkpoint') { return 'last_page'; }
            if(type == 'checkpoint') { return 'flag'; }
            if(type == 'login') { return 'input'; }
            else { return 'ads_click'; }   
        }
    },
    mounted () {
        this.initMoves()
    },
    props: {
        drawer_flag: {},
        steps: {}
    }
  })
  </script>
  