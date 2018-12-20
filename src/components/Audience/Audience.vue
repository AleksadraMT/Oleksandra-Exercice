<template>
  <v-layout row justify-space-between class="audience content-width">
    <v-flex
      class="audience-right"
    >
      <div class="block">
        <label class="app-label">Name your audience</label>
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
      const newArr = [];

      for(let i = 1; i <= 30; i++){
        newArr.push(i); 
      }

      return newArr;
    })(),
    states: [
      "Afghanistan", "Albania", "Algeria", "American Samoa", "Andorra", "Angola", "Anguilla", "Antarctica", "Antigua and Barbuda", "Argentina", "Armenia", "Aruba", "Australia", "Austria", "Azerbaijan", "Bahamas", "Bahrain", "Bangladesh", "Barbados", "Belarus", "Belgium", "Belize", "Benin", "Bermuda", "Bhutan", "Bolivia", "Bosnia and Herzegowina", "Botswana", "Bouvet Island", "Brazil", "British Indian Ocean Territory", "Brunei Darussalam", "Bulgaria", "Burkina Faso", "Burundi", "Cambodia", "Cameroon", "Canada", "Cape Verde", "Cayman Islands", "Central African Republic", "Chad", "Chile", "China", "Christmas Island", "Cocos (Keeling) Islands", "Colombia", "Comoros", "Congo", "Congo, the Democratic Republic of the", "Cook Islands", "Costa Rica", "Cote d'Ivoire", "Croatia (Hrvatska)", "Cuba", "Cyprus", "Czech Republic", "Denmark", "Djibouti", "Dominica", "Dominican Republic", "East Timor", "Ecuador", "Egypt", "El Salvador", "Equatorial Guinea", "Eritrea", "Estonia", "Ethiopia", "Falkland Islands (Malvinas)", "Faroe Islands", "Fiji", "Finland", "France", "France Metropolitan", "French Guiana", "French Polynesia", "French Southern Territories", "Gabon", "Gambia", "Georgia", "Germany", "Ghana", "Gibraltar", "Greece", "Greenland", "Grenada", "Guadeloupe", "Guam", "Guatemala", "Guinea", "Guinea-Bissau", "Guyana", "Haiti", "Heard and Mc Donald Islands", "Holy See (Vatican City State)", "Honduras", "Hong Kong", "Hungary", "Iceland", "India", "Indonesia", "Iran (Islamic Republic of)", "Iraq", "Ireland", "Israel", "Italy", "Jamaica", "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Korea, Democratic People's Republic of", "Korea, Republic of", "Kuwait", "Kyrgyzstan", "Lao, People's Democratic Republic", "Latvia", "Lebanon", "Lesotho", "Liberia", "Libyan Arab Jamahiriya", "Liechtenstein", "Lithuania", "Luxembourg", "Macau", "Macedonia, The Former Yugoslav Republic of", "Madagascar", "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", "Martinique", "Mauritania", "Mauritius", "Mayotte", "Mexico", "Micronesia, Federated States of", "Moldova, Republic of", "Monaco", "Mongolia", "Montserrat", "Morocco", "Mozambique", "Myanmar", "Namibia", "Nauru", "Nepal", "Netherlands", "Netherlands Antilles", "New Caledonia", "New Zealand", "Nicaragua", "Niger", "Nigeria", "Niue", "Norfolk Island", "Northern Mariana Islands", "Norway", "Oman", "Pakistan", "Palau", "Panama", "Papua New Guinea", "Paraguay", "Peru", "Philippines", "Pitcairn", "Poland", "Portugal", "Puerto Rico", "Qatar", "Reunion", "Romania", "Russian Federation", "Rwanda", "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino", "Sao Tome and Principe", "Saudi Arabia", "Senegal", "Seychelles", "Sierra Leone", "Singapore", "Slovakia (Slovak Republic)", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Georgia and the South Sandwich Islands", "Spain", "Sri Lanka", "St. Helena", "St. Pierre and Miquelon", "Sudan", "Suriname", "Svalbard and Jan Mayen Islands", "Swaziland", "Sweden", "Switzerland", "Syrian Arab Republic", "Taiwan, Province of China", "Tajikistan", "Tanzania, United Republic of", "Thailand", "Togo", "Tokelau", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Turks and Caicos Islands", "Tuvalu", "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States", "United States Minor Outlying Islands", "Uruguay", "Uzbekistan", "Vanuatu", "Venezuela", "Vietnam", "Virgin Islands (British)", "Virgin Islands (U.S.)", "Wallis and Futuna Islands", "Western Sahara", "Yemen", "Yugoslavia", "Zambia", "Zimbabwe",
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
