<template>
  <div class="field">
    <label class="label">{{type}}</label>
    <div class="control">
      <div class="select is-fullwidth">
        <select :value="selectedVariationId" @change="changed($event, type)">
          <option value>Please choose</option>
          <option
            :disabled="!variation.in_stock"
            v-for="variation in variations"
            :key="variation.id"
            :value="variation.id"
          >
            {{variation.name}}
            <template v-if="variation.price_varies">({{variation.price}})</template>
            <template v-if="!variation.in_stock">(out of stock)</template>
          </option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      required: true,
      type: String
    },
    variations: {
      required: true,
      type: Array
    },
    value: {
      required: false,
      default: ""
    }
  },
  methods: {
    changed(event, type) {
      this.$emit("input", this.findVariation(event.target.value));
    },
    findVariation(id) {
      const variation = this.variations.find(v => v.id === parseInt(id));

      if (typeof variation === "undefined") return null;

      return variation;
    }
  },
  computed: {
    selectedVariationId() {
      if (!this.value || !this.findVariation(this.value.id)) return "";

      return this.value.id;
    }
  }
};
</script>

<style>
</style>
