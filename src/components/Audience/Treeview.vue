<template>
<div>
  <div class="tree">
    <v-layout>
      <v-flex>
        <div class="tree-title">
          Choose interests
        </div>
        <div v-bar>
          <v-card-text class="tree-container">
            <v-treeview 
              v-model="tree"
              :items="items"
              open-on-click
              selectable
              activatable
              selected-color="#0d6380"
              expand-icon="keyboard_arrow_down"
              on-icon="$vuetify.icons.checkboxOn"
              off-icon="$vuetify.icons.checkboxOff"
              indeterminate-icon="$vuetify.icons.checkboxIndeterminate"
              >
            </v-treeview>         
          </v-card-text>
          <div class="tree-scroll-divider"></div>
        </div>
      </v-flex>
    </v-layout>
  </div>

  <div class="tree-selected">
    <div
      class="empty-block"
      v-if="selections.length === 0"
    >
      You don't have selected items
    </div>
    <v-scroll-x-transition
      group
      hide-on-leave
    >
      <v-chip
        v-for="(selection, id) in selections"
        :key="id"
        :id="selection.id"
        color="grey"
        class="tree-selected-item"
        dark
        small
      >{{selection.name}}<!--
      --><span class="tree-selected-close"><v-icon @click="removeItem(selection.id)">cancel</v-icon></span>
      </v-chip>
    </v-scroll-x-transition>
  </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Vuebar from 'vuebar'; 

Vue.use(Vuebar);

export default {
  name: 'treeview',
  data: () => ({
    tree: [],
    value: [],
    items: [
      {
        id: 1,
        name: 'Animals & Pet Supplies',
        children: [
          { id: 2, name: 'Cat' },
          { id: 3, name: 'Dog' },
          { id: 4, name: 'Rabbit' }
        ]
      },
      {
        id: 5,
        name: 'Arts & Entertainment',
        children: [
          {
            id: 6,
            name: 'Vuetify',
            children: [
              {
                id: 7,
                name: 'Src',
                children: [
                  { id: 8, name: 'Index : ts' },
                  { id: 9, name: 'bootstrap : ts' }
                ]
              }
            ]
          },
          {
            id: 10,
            name: 'material2 :',
            children: [
              {
                id: 11,
                name: 'src :',
                children: [
                  { id: 12, name: 'v-btn : ts' },
                  { id: 13, name: 'v-card : ts' },
                  { id: 14, name: 'v-window : ts' }
                ]
              }
            ]
          }
        ]
      },
      {
        id: 15,
        name: 'Business & Industrial',
        children: [
          { id: 16, name: 'October : pdf' },
          { id: 17, name: 'November : pdf' },
          { id: 18, name: 'Tutorial : html' }
        ]
      },
      {
        id: 19,
        name: 'Videos :',
        children: [
          {
            id: 20,
            name: 'Tutorials :',
            children: [
              { id: 21, name: 'Basic layouts : mp4' },
              { id: 22, name: 'Advanced techniques : mp4' },
              { id: 23, name: 'All about app : dir' }
            ]
          },
          { id: 24, name: 'Intro : mov' },
          { id: 25, name: 'Conference introduction : avi' }
        ]
      },
      {
        id: 26,
        name: 'Cameras & Optics',
        children: [
              { id: 27, name: 'Basic layouts : mp4' },
              { id: 28, name: 'Advanced techniques : mp4' },
              { id: 29, name: 'All about app : dir' }
            ]
      },
      {
        id: 30,
        name: 'Appeal & Accessories',
        children: [
              { id: 31, name: 'Basic layouts : mp4' },
              { id: 32, name: 'Advanced techniques : mp4' },
              { id: 33, name: 'All about app : dir' }
            ]
      },
      {
        id: 34,
        name: 'Electronics',
        children: [
              { id: 35, name: 'Basic layouts : mp4' },
              { id: 36, name: 'Advanced techniques : mp4' },
              { id: 37, name: 'All about app : dir' }
            ]
      },
      {
        id: 38,
        name: 'For children',
        children: [
              { id: 39, name: 'Basic layouts : mp4' },
              { id: 40, name: 'Advanced techniques : mp4' },
              { id: 41, name: 'All about app : dir' }
            ]
      },
      {
        id: 42,
        name: 'More',
        children: [
              { id: 43, name: 'Basic layouts : mp4' },
              { id: 44, name: 'Advanced techniques : mp4' },
              { id: 45, name: 'All about app : dir' }
            ]
      }
    ],
  }),
  computed: {
    selections: {
      get: function() {
        const selections = [];
        const getChildren = (element, idx) => {
        element.forEach(element => {
          if (element.id === idx) {
            selections.push(element);
          }
          if (!element.children) {
            return;
          } else {
            getChildren(element.children, idx);
          }
        });
      };

      for (const leaf of this.tree) {
        getChildren(this.items, leaf);
      }

      return selections;
      },
    }
  },

  methods:{
    removeItem(id) {
      let parentsArr = [];
      let flag = false;

      const newTree = (idArr) => this.tree.filter(val => {
        return idArr.indexOf(val) === -1;
      });

      const getAllChildren = (items) => {
        items.forEach(element => {
          parentsArr.push(element.id);

          if(element.children) {
            getAllChildren(element.children);
          } else {
            return;
          }
        });
      }

      const checkChildren = (items) => {
        items.forEach(element => {

          if (flag) return;

          if (element.id === id) {
            parentsArr.push(element.id);
            flag = true;

            if (element.children) {
              getAllChildren(element.children);
            }
          } else {
            if (element.children) {

              parentsArr.push(element.id);

              checkChildren(element.children);
            }
          }
        });
      }
      checkChildren(this.items);

      this.tree = newTree(parentsArr);
    },
  }
}
</script>

<style lang="scss">
@import './../../assets/scss/variables.scss';

.tree {
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 7px 1px rgba(0, 0, 0, .1);

  &-title {
    font-weight: 500;
    font-size: 14px;
    padding: 8px 20px;
    border-bottom: 1px solid $greyColor;
  }

  &-container {
    padding: 20px 0 20px 21px;
    max-height: 240px;
    // overflow-y: auto;
    position: relative;

    &.v-treeview-node__label {
      font-size: 15px;
    }

    .v-treeview-node__root {
      height: 40px;
    }

    .v-treeview-node__toggle {
      color: $fontColor;
      font-size: 20px;
      width: 19px;
      height: 19px;
    }

    .v-treeview-node__label {
      font-size: 14px;
      margin-left: 7px;
    }
  }

  &-scroll-divider {
    position: absolute;
    width: 1px;
    height: 100%;
    background-color: $greyColor;
    right: 18px;
    top: 0;
    bottom: 0;
  }

  &-selected-item {
    height: 30px;
    margin: 10px 10px 0 0;
    background-color: $greyColor !important;
    border-color: $greyColor !important;
    font-size: 14px;

    .v-chip__content {
      padding: 0 19px;
    }
  }

  &-selected-close {
    .v-icon {
      margin-left: 4px;
      margin-right: -18px;
      color: #e9ebeb;
      position: relative;
      font-size: 25px;
      cursor: pointer;

      &:after {
        content: '';
        position: absolute;
        width: calc(100% - 10px);
        height: calc(100% - 10px);
        background-color: #1d1e1e;
        right: calc(50% - 8px);
        top: calc(50% - 7px);
        z-index: -1;
        border-radius: 100%;
      }

      &:hover {
        color: lighten($greyColor, 50%);
      }
    }
  }
}

.empty-block {
  padding: 10px 0;
  color: $greyColor;
  font-size: 15px;
}

// Custom Scroll Style

.vb {
  .vb-dragger {
    z-index: 5;
    width: 19px;
    right: 0;
  }
}

.vb > .vb-dragger > .vb-dragger-styler {
    backface-visibility: hidden;
    transform: rotate3d(0, 0, 0, 0);
    transition: background-color 100ms ease-out, margin 100ms ease-out, height 100ms ease-out;
    background-color: #868a8a;
    margin: 4px 3px 0px 5px;
    border-radius: 3px;
    height: calc(100% - 8px);
    display: block;
}
</style>
