<template>
  <div>
    <h2>see console for vue 2 lifecycle messages</h2>
    <p>{{ msg }}</p>
    <button @click="click()">update</button>
    <BadComponent />
  </div>
</template>

<script>
import BadComponent from "./BadComponent.vue";

export default {
  data() {
    return {
      msg: "before hello",
      stateOfBob: "sleeping",
    };
  },
  components: {
    BadComponent,
  },
  methods: {
    oops() {
      throw new Error("oops");
    },
    click(){
      this.msg="Updated msg"
    }
  },
  beforeCreate() {
    console.log("beforeCreate==== I'm beforeCreate hook");
    console.log("beforeCreate==== Bob is currently", this.stateOfBob);
  },

  created() {
    console.log("Created====  Bob is currently", this.stateOfBob);
    this.stateOfBob = "awakened but still sleeping";
    console.log("Created==== Bob is currently ", this.stateOfBob);
  },
  beforeMount() {
    // mount hooks do NOT run during server-side render
    // use if need to access/modify DOM
    console.log("Lifecycle: beforeMount", this.$el);
  },
  mounted() {
    // full access to reactive component, templates,
    // and rendered dome via this.$el
    // used to integrate non-Vue libs
    console.log("Lifecycle: mounted", this.$el);
  },
  beforeUpdate() {
    // this.msg="demo"
    // update hooks called when reactive prop / state changes
    console.log("Lifecycle: beforeUpdate====",this.msg);
  },
  updated() {
    // this.demo="temp"
    console.log("Lifecycle: updated==",this.msg);
  },
  beforeDestroy() {
    // destruction hooks used for cleanup, analytics seeding
    console.log("Lifecycle: beforeDestroy");
  },
  destroyed() {
    // any last minute stuff (like inform remote server)
    // console.log("Lifecycle: destroyed");
  },
  errorCaptured(err, component, details) {
    console.log("error captured====",err, component, details);
  },
  
};
</script>
