<template>
  <div>
    <PageHeader text="患者データ一覧" :is-logged-in="true" />
    <div class="searchContainer">
      <SearchField :value="inputSearch" @input="inputSearch = $event" />
      <SortSelect v-model="itemSelect" />
    </div>
    <div class="overviewContainer">
      <table class="overviewTable">
        <thead>
          <tr class="overviewTableHeader">
            <th>患者ID</th>
            <th>最終更新</th>
            <th>SpO2</th>
            <th>体温/脈拍</th>
            <th></th>
            <th>症状</th>
          </tr>
        </thead>
        <tbody>
          <PatientOverview
            v-for="(patient, index) in patients"
            :key="index"
            :patient="patient"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import PageHeader from '@/components/PageHeader.vue'
import PatientOverview from '@/components/PatientOverview.vue'
import SearchField from '@/components/SearchField.vue'
import SortSelect from '@/components/SortSelect.vue'

export default Vue.extend({
  name: 'Index',
  components: {
    PageHeader,
    PatientOverview,
    SearchField,
    SortSelect,
  },
  data() {
    return {
      inputSearch: '',
      itemSelect: 'latest',
      patients: [
        {
          patientId: 'string',
          centerId: 'string',
          policy_accepted: '2021-01-17T05:09:12.935Z',
          phone: 'string',
          display: true,
          statuses: [
            {
              statusId: 'string',
              patientId: 'string',
              centerId: 'string',
              created: '2021-01-17T05:09:12.935Z',
              SpO2: 0,
              body_temperature: 0,
              pulse: 0,
              symptom: {
                symptomId: 'string',
                cough: true,
                phlegm: true,
                suffocation: true,
                headache: false,
                sore_throat: true,
                remarks: '本日はどうも体調が優れません。',
              },
            },
          ],
        },
      ],
    }
  },
})
</script>

<style lang="scss" scoped>
.searchContainer {
  margin: 16px 0;
}
.overviewContainer {
  background-color: $white;
  border-radius: 8px;
  overflow: hidden;
}
.overviewTable {
  width: 100%;
  border-spacing: 0;
  tbody tr {
    border-bottom: 1px solid $gray-3;
    padding: 8px 0;
    &:last-child {
      border: none;
    }
  }
}
.overviewTableHeader {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 30% 24%;
  grid-template-rows: auto;
  font-size: 16px;
  color: $gray-3;
  border-bottom: 1px solid $gray-3;
  padding: 8px 0;
}
</style>
