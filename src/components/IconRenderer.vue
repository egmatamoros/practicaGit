<template>
  <div>
    <svg
      width="50px"
      height="50px"
      viewBox="0 0 512 512"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path :d="iconData"></path>
    </svg>
    <div>
      {{ name }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    icon: {
      type: Array,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
  },
  computed: {
    iconWidth() {
      return this.icon[0];
    },
    iconHeight() {
      return this.icon[1];
    },
    iconData() {
      return this.icon[4];
    },
  },
};
</script>
