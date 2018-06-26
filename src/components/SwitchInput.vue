<template>
  <div class="switch-input"
    @click="toggleCheck" 
    :class="{checked: isChecked, disabled: disabled}">
    <div class="switch"></div>
    <input type="checkbox" :name="name" :value="value" :checked="isChecked"/>
  </div>
</template>

<script>
export default {
  name: "switch-input",
  model: {
    prop: "modelValue",
    event: "change"
  },
  props: {
    value: {
      default: true
    },
    modelValue: {
      default: false
    },
    name: {
      type: String,
      default: ""
    },
    trueValue: {
      default: true
    },
    falseValue: {
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  mounted() {},
  computed: {
    isChecked() {
      if (this.modelValue instanceof Array) {
        return this.modelValue.includes(this.value);
      }
      return this.modelValue === this.trueValue;
    }
  },
  watch: {
    modelValue(val) {
      console.log(val, this.$el);
    }
  },
  methods: {
    toggleCheck(event) {
      if (this.disabled) {
        return;
      }

      let isChecked = !this.isChecked;

      if (this.modelValue instanceof Array) {
        let newValue = [...this.modelValue];

        if (isChecked) {
          newValue.push(this.value);
        } else {
          newValue.splice(newValue.indexOf(this.value), 1);
        }

        this.$emit("change", newValue);
      } else {
        this.$emit("change", isChecked ? this.trueValue : this.falseValue);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.switch-input {
  margin: 2px 0px;
  width: 50px;
  height: 25px;
  border: 2px solid #ddd;
  background: #ddd;
  border-radius: 25px;
  box-sizing: border-box;
  position: relative;
  cursor: pointer;
  display: inline-block;
  vertical-align: middle;

  .switch {
    width: 50%;
    height: 100%;
    box-sizing: border-box;
    margin-left: 0px;
    background: #fff;
    border-radius: 50%;
    transition: margin 0.2s ease-out;
    margin-left: 0px;
  }

  &:not(.disabled):hover {
    .switch {
      box-shadow: 0px 0px 0px 4px rgba(0, 0, 0, 0.1);
    }
  }

  &.checked {
    background-color: #00aad4;
    border-color: #00aad4;
    .switch {
      margin-left: 50%;
      background-color: #fff;
    }
  }

  &.disabled {
    opacity: 0.5;
    cursor: default;
  }

  input {
    display: none;
  }
}
</style>
