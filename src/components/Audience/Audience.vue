<template>
  <v-layout row justify-space-between class="audience content-width">
    <v-flex
      class="audience-right"
    >
      <div class="block">
        <label class="app-label" for="audience-name">Name your audience</label>
        <v-text-field
          class="app-input app-input-small"
          placeholder="Audience name"
          hide-details       
          solo
        ></v-text-field>
      </div>
      <div class="block">
        <label class="app-label">Choose country</label>
        <v-autocomplete
          v-model="model"
          :items="states"
          class="app-input app-input-small"
          append-icon=""
          placeholder="Type here"
          persistent-hint
          hide-details
          solo
        ></v-autocomplete>
      </div>
      <div class="block block-small">
        <Treeview />
      </div>
      <div class="exclude block block-small">
        <div class="exclude-title app-title">
          Exclude your visitors
        </div>
        <p class="exclude-text">All buyers of your website or app are automatically excluded.</p>
        <p class="exclude-text">Exclude users who visited your web site or app in the last 
          <v-select
            v-model="selectedDays"
            :items="items"
            hide-details
            outline
            solo
            color="#0d6380"
            class="app-select exclude-select"
          ></v-select>
           Days
          </p>
      </div>
    </v-flex>
    <v-flex 
      class="audience-left"
    >
      <Range />
    </v-flex>
  </v-layout>   
</template>

<script>
import Treeview from './Treeview';
import Range from './Range';

export default {
  name: 'Audience',
  components: {
    Treeview,
    Range,
  },
  data: () => ({
    audienceValue: `Reengage-audience-2017`,
    country: `France`,
    isEditing: false,
    model: null,
    selectedDays: 30,
    items: (() => {
      var newArr = [];

      for(var i = 1; i <= 30; i++){
        newArr.push(i); 
      }

      return newArr;
    })(),
    states: [
      'Alabama', 'Alaska', 'American Samoa', 'Arizona',
      'Arkansas', 'California', 'Colorado', 'Connecticut',
      'Delaware', 'District of Columbia', 'Federated States of Micronesia',
      'Florida', 'Georgia', 'Guam', 'Hawaii', 'Idaho',
      'Illinois', 'Indiana', 'Iowa', 'Kansas', 'Kentucky',
      'Louisiana', 'Maine', 'Marshall Islands', 'Maryland',
      'Massachusetts', 'Michigan', 'Minnesota', 'Mississippi',
      'Missouri', 'Montana', 'Nebraska', 'Nevada',
      'New Hampshire', 'New Jersey', 'New Mexico', 'New York',
      'North Carolina', 'North Dakota', 'Northern Mariana Islands', 'Ohio',
      'Oklahoma', 'Oregon', 'Palau', 'Pennsylvania', 'Puerto Rico',
      'Rhode Island', 'South Carolina', 'South Dakota', 'Tennessee',
      'Texas', 'Utah', 'Vermont', 'Virgin Island', 'Virginia',
      'Washington', 'West Virginia', 'Wisconsin', 'Wyoming', 'France'
    ]
  }),
}
</script>

<style lang="scss">
.audience {
  padding: 37px 30px 32px;
  &-right {
    width: 100%;
  }

  &-left {
    margin-left: 40px;
    position: relative;
    top: -96px;
  }
}

.block {
  margin-top: 58px;

  &-small {
    margin-top: 38px;
  }

  &:first-child {
    margin-top: 0;
  }
}

.exclude {
  &-text {
    margin-bottom: 8px;
  }
  &-title {
    padding-bottom: 4px;
  }
  &-select.v-text-field {
    display: inline-block;
    width: 60px;
    margin: 0 6px 0 8px;
  }
}
.v-btn {
    padding: 0 21px;
}
</style>
