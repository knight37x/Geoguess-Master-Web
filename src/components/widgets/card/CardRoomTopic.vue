<template>
  <v-card color="#061422">
    <v-card-title>
      <span id="card-title">{{ $t('CardRoomTopic.title') }}</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-select
              dark
              v-model="roomTopic"
              :items="roomTopicItems"></v-select>
        </v-row>
        <v-row v-if="roomTopic === 'custom'">
          <input id="custom-input" v-model="customTopic" :placeholder="$t('CardRoomTopic.customPlaceholder')">
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions>
      <div class="flex-grow-1"></div>
      <v-btn
        dark
        depressed
        color="#43B581"
        @click="setRoomTopic">{{ $t('CardRoomTopic.next') }}</v-btn>
      <v-btn
        dark
        depressed
        color="#FF5252"
        @click="cancel">{{ $t('CardRoomTopic.cancel') }}</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
  import Vue from 'vue'
  import {TranslateResult} from "vue-i18n";

  declare interface RoomTopicItem {
    text: string | TranslateResult,
    value: string,
  }

  export type DataType = {
    roomTopic: string,
    roomTopicItems: RoomTopicItem[],
    customTopic: string,
  }

  export default Vue.extend({
    name: 'CardRoomTopic',

    data(): DataType {
      return {
        roomTopic: 'random',
        roomTopicItems: [
          {
            text: this.$t('CardRoomTopic.random'),
            value: 'random',
          },
          {
            text: this.$t('CardRoomTopic.poiWorld'),
            value: 'places in world',
          },
          {
            text: this.$t('CardRoomTopic.poiEurope'),
            value: 'places in europe',
          },
          {
            text: this.$t('CardRoomTopic.poiUSA'),
            value: 'places in usa',
          },
          {
            text: this.$t('CardRoomTopic.poiRussia'),
            value: 'places in russia',
          },
          {
            text: this.$t('CardRoomTopic.poiAsia'),
            value: 'places in asien', // we need to write this otherwhise results are wrong
          },
          {
            text: this.$t('CardRoomTopic.poiAustralia'),
            value: 'places in australia',
          },
          {
            text: this.$t('CardRoomTopic.castlesEurope'),
            value: 'castles in europe',
          },
          {
            text: this.$t('CardRoomTopic.custom'),
            value: 'custom',
          },
        ],
        customTopic: '',
      }
    },

    methods: {
      setRoomTopic(): void {
        this.$emit('setRoomTopic', this.roomTopic === 'custom' ? this.customTopic : this.roomTopic)
      },

      cancel(): void {
        this.$emit('cancel')
      }
    }
  })
</script>

<style scoped>
  #card-title {
    font-size: 16px;
    font-weight: 500;
    color: #FFFFFF;
    opacity: 0.9;
  }
  #custom-input {
    color: #FFFFFF;
    width: 100%;
  }
</style>