<template>
  <div id="soundsTabBody">
    Checking the checkbox next to an option will allow a sound to be played for those new items.

    <div class="tab-wrap fit-height pt-3">
      <b-form-group label="Sound Filters">
        <b-form-checkbox-group
          id="sound-checks"
          name="Sound Filters"
          :options="options"
          v-model="activeSounds"
          v-on:change="(vals) => updateSounds(vals)"
          switches
          stacked
          class="settings-group"
        >
        </b-form-checkbox-group>
      </b-form-group>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  name: 'SoundOptionsTab',
  data() {
    return {
      options: [
        {
          value: 'night',
          text: 'Eidolon Roar to Start the Night',
        },
        {
          value: 'alert',
          text: 'Alert tone',
        },
        {
          value: 'invasion',
          text: 'Invasion Tone',
        },
      ],
    };
  },
  computed: {
    ...mapGetters('worldstate', ['sounds']),
    activeSounds: {
      get: function () {
        return JSON.parse(JSON.stringify(this.sounds));
      },
      set: function () {},
    },
  },
  methods: {
    updateSounds(enabledSounds) {
      this.$store.commit('worldstate/commitSounds', [JSON.parse(JSON.stringify(enabledSounds))]);
    },
  },
};
</script>
