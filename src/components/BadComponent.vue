<template>
  <div>
    <p>click to throw error, examine console</p>
    <button @click="oops">throw error</button>
  </div>
</template>

<script>
export default {
  methods: {
    oops() {
      throw new Error("oops");
    }
  }
};
</script>
