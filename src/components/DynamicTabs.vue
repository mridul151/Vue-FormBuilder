<template>
  <v-app>
    <v-tabs v-model="mainActiveTab">
      <v-tab v-for="(tab, index) in mainTabs" :key="index">{{ tab.title }}</v-tab>
    </v-tabs>
    <v-tab-items v-model="mainActiveTab">
      <v-tab-item v-for="(tab, index) in mainTabs" :key="index">
        <component :is="tab.component" :data="tabData"></component>
      </v-tab-item>
    </v-tab-items>
    <v-btn @click="viewDetails" color="primary">View Details</v-btn>
    <v-dialog v-model="modalOpen" fullscreen>
      <v-card>
        <v-card-title>
          <v-tabs v-model="activeTab">
            <v-tab key="layout">Layout</v-tab>
            <v-tab key="preview">Preview</v-tab>
          </v-tabs>
          <v-spacer></v-spacer>
          <v-btn icon @click="closeModal">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text>
          <v-tab-items v-model="activeTab">
            <v-tab-item key="layout">
              <!-- Layout content here -->
<div v-for="(comp, index) in layoutComponents" :key="index">
      <component :is="comp"></component>
    </div>
            </v-tab-item>
            <v-tab-item key="preview">
              <!-- Preview content here -->
            </v-tab-item>
          </v-tab-items>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="openSidebar('component')" color="primary">New Component</v-btn>
          <v-btn @click="openSidebar('resource')" color="primary">New Resource</v-btn>
        </v-card-actions>

        <v-navigation-drawer v-model="sidebarOpen" right absolute>
          <v-list>
            <v-list-item-group>
              <v-list-item @click="closeSidebar">
                <v-list-item-title>Close Sidebar</v-list-item-title>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>Create New {{ sidebarType }}</v-list-item-title>
                  <v-select
                    v-if="sidebarType === 'component'"
                    v-model="selectedComponent"
                    :items="availableComponents"
                    label="Select a component"
                    outlined
                  ></v-select>
                </v-list-item-content>
                <v-list-item-action>
                  <v-btn color="primary" @click="addComponent" :disabled="!selectedComponent">Add</v-btn>
                </v-list-item-action>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-navigation-drawer>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import axios from 'axios';
import VForm from '../components/VForm.vue';
import VTextField from '../components/VTextField.vue';
import VButton from '../components/VButton.vue';

export default {
  components: {
    VForm,
    VTextField,
    VButton,
    // Import and register other Vuetify components here
  },
  data() {
    return {
      modalOpen: false,
      mainTabs: [],
      mainActiveTab: 0,
      activeTab: 'layout',
      sidebarOpen: false,
      sidebarType: 'component',
      tabData: {},
      availableComponents: ['VForm', 'VTextField', 'VButton'],
      selectedComponent: null,
      selectedComponentObject: null,
      layoutComponents: []
    };
  },

  methods: {
    viewDetails() {
      this.modalOpen = true;
    },
    closeModal() {
      this.modalOpen = false;
    },
    openSidebar(type) {
      this.sidebarType = type;
      this.sidebarOpen = true;
    },
    closeSidebar() {
      this.sidebarOpen = false;
      this.selectedComponent = null;
      this.selectedComponentObject = null;
    },
    addComponent() {

    let comp={
    "Vform":VForm,
    "VTextField":VTextField,
    "VButton":VButton
    };

    if (this.selectedComponent) {
    // Fix the typo here
    this.layoutComponents.push(comp[this.selectedComponent]);
  }
  this.closeSidebar();
    },
    fetchMainTabsData() {
      axios.get('https://run.mocky.io/v3/36ec4c74-ca38-4ae0-b671-65238d2e9e3d')
        .then(response => {
          const navigationData = response.data.navigationData;
          this.mainTabs = navigationData.navigation.map(nav => {
            return {
              title: nav.title,
              component: {
                template: `<div>${nav.title} content</div>`
              }
            };
          });
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    }
  },

  mounted() {
    this.fetchMainTabsData();
  }
};
</script>
