<template>
    <div class="full child container rounded-1 light-1-glass grey-square q-pa-xs q-mb-xs">
        <div class="nasalization font-8 row rounded-1 q-py-xs q-px-sm">
            <div class="col text-left">
                <q-btn 
                    flat
                    align="left"
                    size="sm"
                    icon="label_important"
                    :label="taglist[enabled - pos]"
                    class="q-pa-sm q-pl-md rounded-2 inset-font"
                />
            </div>
            <div class="col text-right q-pt-sm">
                <span class="q-px-sm text-grey-13">{{ '[' + taglist[enabled - pos + 1] + "'s son]" }}</span>
            </div>
        </div>
        <div v-if="(pos < taglist.length && pos < enabled)" class="full child container column child rounded-1 q-pa-sm">
            <TagNester :taglist="taglist" :enabled="enabled" :pos="pos + 1" ></TagNester>
        </div>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  
  export default defineComponent({
    name: 'TagNester',
    data () {
        return {
            enabled_flag: this.enabled,
            pos_flag: this.pos
        }
    },
    props: {
        taglist: {},
        enabled: {},
        pos: {}
    }
  })
  </script>
  