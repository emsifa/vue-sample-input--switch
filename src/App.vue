<template>
  <div id="app">
    <img width="20%" src="./assets/logo.png">
    <div class="examples">
      <p>
        Single Value
        <switch-input v-model="single" name="single"/>: {{ single }}
        
        <br/>
        Single with Custom Value
        <switch-input v-model="something" name="something" true-value="foo" false-value="bar"/>: {{ something }}

        <br/>
        Disabled
        <switch-input :disabled="true" v-model="something" name="something" true-value="foo" false-value="bar"/>: {{ something }}
      </p>
      <p>
        Array Value
        <br>
        1: <switch-input v-model="array" value="1" name="array[]"/>
        <br>
        2: <switch-input v-model="array" value="2" name="array[]"/>
        <br>
        3: <switch-input v-model="array" value="3" name="array[]"/>
        <br>
        4: <switch-input v-model="array" value="4" name="array[]"/>
        <br>
        5: <switch-input v-model="array" value="5" name="array[]"/>
        <br>
        <code>{{ array }}</code>
      </p>
    </div>
  </div>
</template>

<script>
import SwitchInput from "./components/SwitchInput";

export default {
  name: "App",
  components: {
    SwitchInput
  },
  data() {
    return {
      single: true,
      something: "foo",
      array: []
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 100%;
}
.examples {
  text-align: left;
  width: 300px;
  margin: auto;
}
</style>
