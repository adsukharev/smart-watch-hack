<template>
  <div class="pa-6">
    <div>
      <div class="text-h3" v-text="headerText"></div>
      <div class="header-divider"></div>
    </div>
    <v-tabs color="gray" @change="onTabsChange">
      <v-tab>Общие сведения</v-tab>
      <v-tab>Организационно-штатная структура</v-tab>
      <v-tab>Объекты</v-tab>
    </v-tabs>
    <company-info v-show="currentTabIndex === 0" :company="company" />
    <company-employee v-show="currentTabIndex === 1" :employee="employee" />
    <company-objects v-show="currentTabIndex === 2" :objects="objects" />
  </div>
</template>

<script>
import { has } from 'lodash';
import CompanyInfo from '@/components/CompanyInfo.vue';
import CompanyEmployee from '@/components/CompanyEmployee.vue';
import CompanyObjects from '@/components/CompanyObjects.vue';

export default {
  name: 'Company',
  components: {
    CompanyInfo,
    CompanyEmployee,
    CompanyObjects
  },
  data() {
    return {
      headerText: '',
      company: null,
      employee: [],
      objects: [],
      currentTabIndex: 0
    };
  },
  created() {
    // this.headerText = this.$route.params.id;
    // // fetch company

    // Don't ever do like this
    if (has(this.$route, 'params.name')) {
      this.headerText = this.$route.params.name;
    } else {
      this.headerText = 'Организация 1';
    }
  },
  methods: {
    onTabsChange(index) {
      console.log(index);
      this.currentTabIndex = index;
    }
  }
};
</script>

<style lang="scss" scoped>
.header-divider {
  height: 2px;
  width: 100%;
  background-color: #fb2424;
}
</style>
