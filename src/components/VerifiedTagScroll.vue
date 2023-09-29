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
                    <div class="q-pa-none shadow-1 rounded-1" style="min-width: 60px;">
                        <q-btn
                            no-caps
                            dense
                            flat
                            size="xs"
                            class="q-pa-xs full-width bg-grey-12"
                        >
                            <div class="ellipsis full-width q-pa-none row">
                                <div class="col-1 q-pr-sm"><q-icon :name="tag.icon" size="1.5em"/></div>
                                <div class="col">{{ tag.label }}</div>
                            </div>
                            <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                                <div class="col-1 q-pr-md">
                                    <q-icon :name="tag.icon" size="1.2em"/>
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
    name: 'VerifiedTagScroll',
    data () {
        return {
            background_tags: [
                { label: "August 27", icon: "calendar_month", src: "node/c51043cb1e55b93cbb7929d81c2d43cb1e5" },
                { label: "01:33 AM", icon: "schedule", src: "node/c51043cb1e55b93cbb7929d81c2d43cb1e5" },
                { label: "Earth Planet", icon: "location_on", src: "node/c51043cb1e55b93cbb7929d81c2d43cb1e5" }
            ],
            // baseURL: axios.get(process.env.VUE_APP_BASE_URL + 'img/')
        }
    }
  })
  </script>