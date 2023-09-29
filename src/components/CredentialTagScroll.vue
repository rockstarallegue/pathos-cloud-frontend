<template>
    <div class="fit q-pa-none">
        <q-scroll-area class="q-pa-none fit">
            <div class="row no-wrap rounded-1 q-pa-none q-px-xs">
                <div v-for="(credential, n) in credentials" :key="n" class="q-mr-sm">
                    <div class="q-pa-none rounded-1 shadow-1">
                        <q-btn-group flat>
                            <q-btn
                                no-caps
                                dense
                                flat
                                size="xs" 
                                class="inset-font q-pa-xs bg-grey-12"
                            >
                                <q-avatar v-if="credential.avatar != ''" rounded style="height: 0.3em; width:0.3em">
                                    <img :src="credential.avatar">
                                </q-avatar>
                                <q-icon v-if="credential.avatar == ''" :name="getIcon(credential.type)" size="1.8em"/>
                                <q-tooltip class="bg-grey-13 text-dark-blue inset-font">
                                    <div class="text-center text-black">
                                        {{ credential.type }}: {{ credential.title }}
                                    </div>
                                    {{ credential.direction }}
                                </q-tooltip>
                                
                            </q-btn>
                            <q-btn-dropdown 
                                v-if="credential.milestones.length > 0 || credential.roles.length > 0"
                                no-caps
                                dense
                                flat
                                size="xs" 
                                class="inset-font q-pa-none bg-grey-12"
                            >
                                <q-list class="bg-grey-13">
                                    <!-- ROLES -->
                                    <q-item
                                        v-for="(role, s) in credential.roles"
                                        :key="s"
                                        clickable 
                                        v-close-popup 
                                        @click="onItemClick"
                                        class="q-pa-none"
                                    >
                                        <q-item-section avatar class="text-center q-pl-md">
                                            <q-icon v-if="role.avatar == ''" class="inset-font text-dark-blue q-pa-xs bg-grey-12 rounded-2" name="badge" size="sm"/>
                                            <q-avatar v-if="role.avatar != ''" rounded style="height: 0.6em; width:0.6em" class="bg-grey-12 q-pa-none">
                                                <img :src="role.avatar" style="height: 1em; width:1em">
                                            </q-avatar>
                                        </q-item-section>
                                        <q-separator vertical></q-separator>
                                        <q-item-section class="q-px-sm">
                                            <q-item-label> {{ role.title }}</q-item-label>
                                            <q-item-label caption> {{ role.date }}</q-item-label>
                                        </q-item-section>
                                    </q-item>
                                    <q-separator></q-separator>
                                    <!-- MILESTONES -->
                                    <q-item
                                        v-for="(milestone, m) in credential.milestones"
                                        :key="m"
                                        clickable 
                                        v-close-popup 
                                        @click="onItemClick"
                                        class="q-pa-none"
                                    >
                                        <q-item-section avatar class="text-center q-pl-md">
                                            <q-icon v-if="milestone.avatar == ''" class="inset-font text-dark-blue q-pa-xs bg-grey-12 rounded-2" name="tour" size="sm"/>
                                            <q-avatar v-if="milestone.avatar != ''" rounded style="height: 0.6em; width:0.6em" class="bg-grey-12 q-pa-none">
                                                <img :src="milestone.avatar" style="height: 1em; width:1em">
                                            </q-avatar>
                                        </q-item-section>
                                        <q-separator vertical></q-separator>
                                        <q-item-section class="q-px-sm">
                                            <q-item-label> {{ milestone.title }}</q-item-label>
                                            <q-item-label caption> {{ milestone.date }}</q-item-label>
                                        </q-item-section>
                                    </q-item>
                                </q-list>
                            </q-btn-dropdown>
                        </q-btn-group>
                        
                    </div>
                </div>
            </div>
        </q-scroll-area>
    </div>
</template>
  
  <script>
  import { defineComponent } from 'vue'
  
  export default defineComponent({
    name: 'CredentialTagScroll',
    data () {
        return {
            credentials: [
                { type: 'Organisation', title: 'ITESM', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/265314264-782331a1-57d8-480b-a600-5876d6ac8a8d.png', milestones: [], roles: [ { title: 'Student, ITC', direction: 'roles/b93cbb7929', date: 'Since Aug 2019', avatar: '' }] },
                { type: 'Profile', title: 'Twitter profile', direction: 'https://twitter.com/ll3gu3', avatar: 'https://user-images.githubusercontent.com/52062448/263512473-792d10ac-f79a-4761-bf39-5df42fab2268.png', milestones: [], roles: [] },
                { type: 'Community', title: 'Visual Artists', direction: 'communities/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', avatar: '', milestones: [], roles: [ { title: 'Giphy Celebrity', direction: 'roles/b93cbb7929', date: 'Sept 16 2023', avatar: 'https://gist.githubusercontent.com/all3gu3/3126984111902cd03a661716d222321d/raw/dea861e0131b94c2139ce1b2da22959f8af8b520/giphy-mini.svg' } ] },
                { type: 'Organisation', title: 'UAEM', direction: 'organisations/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', avatar: 'https://user-images.githubusercontent.com/52062448/265314338-aa8817d6-ae49-4162-a2fc-3fb2d52e6520.png', milestones: [ { title: 'Handball team student', direction: 'milestones/b93cbb7929', date: 'Aug 16 2023', avatar: '' }, { title: 'High School diploma', direction: 'milestones/n73cbb7929', date: 'Sept 16 2023', avatar: '' } ], roles: [ { title: 'Ex-Student', direction: 'milestones/n73cbb7929', date: 'Sept 16 2023', avatar: '' } ]}
                // { type: 'Profile', title: 'Denisse Garcia', direction: 'users/f39857vf1e55b93cbb7929d81c2d11de022a60ace7d7a767c6d36a2cf67ca173', avatar: '', milestones: [], roles: [] },
            ]
            // baseURL: axios.get(process.env.VUE_APP_BASE_URL + 'img/')
        }
    },
    methods: {
        getIcon (type) {
            if(type=='Profile'){ return "face_5" }
            if(type=='Community'){ return "diversity_2" }
            if(type=='Organisation'){ return "reduce_capacity" }
            else{ return '' }
        }
    }
  })
  </script>
  