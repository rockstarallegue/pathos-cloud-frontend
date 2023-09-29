<template>
    <div class="fit q-pa-none">
        <q-scroll-area class="q-pa-none fit">
            <div class="row no-wrap rounded-1 q-pa-none q-px-xs">
                <div v-for="(tag, n) in background_tags" :key="n" class="q-mr-xs">
                    <!-- div class="q-pa-none rounded-1 neon-rate shadow-1">
                        <q-chip square size="xs" class="nasalization inset-font bg-grey-11" icon="label_important">
                            {{ tag.label }}
                        </q-chip>
                    </div-->
                    <div class="q-pa-none shadow-1 rounded-1" style="min-width: 70px;">
                        <q-btn
                            no-caps
                            dense
                            flat
                            size="xs"
                            class="q-px-xs full-width bg-grey-12"
                        >
                            <div class="ellipsis full-width q-pa-none row">
                                <div class="col-1 q-pr-md"><q-icon name="label_important" size="1.5em"/></div>
                                <div class="col">{{ tag.label }}</div>
                            </div>
                            <div 
                                class="full-width q-pa-none rounded-1" 
                                :style="getRankingLine(tag.up, tag.down)">
                            </div>
                            <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                                <div class="col-1 q-pr-md">
                                    <q-icon name="label_important" size="1.2em"/>
                                    {{ tag.label }}
                                </div>
                                <div class="ellipsis text-center text-black" style="max-width: 200px;">
                                    {{ tag.src }}
                                </div>
                            </q-tooltip>
                            
                        </q-btn>
                    </div>
                </div>
            </div>
        </q-scroll-area>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  // import TagList from 'src/components/TagList.vue'
  // import MarkdownItem from 'src/components/MarkdownItem.vue'
  
  export default defineComponent({
    name: 'RankedTagScroll',
    data () {
        return {
            background_tags: [
                { label: "Content", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 2, down: 10 },
                 { label: "Pixel Art", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 2, down: 7 },
                { label: "RGB", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 8, down: 4 },
                { label: "RGB", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 20, down: 5 },
                { label: "Long tag that takes a lot of space", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 10, down: 10 }
            // { label: "Long tag that takes even more space than the tag before", src: 'tag/c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173-c51043cb1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', url: "https://twitter.com/Guandanarian", up: 12, down: 5 }
            ],
            // baseURL: axios.get(process.env.VUE_APP_BASE_URL + 'img/')
        }
    },
    methods: {
        getRankingLine(up, down){
            var green = parseInt(up*100/(up+down) - 5)
            var red = parseInt(100 - (down*100/(up+down)) + 5)
            var line = "height:2px; background: linear-gradient(90deg, rgba(205,220,57,1) " + 
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
  