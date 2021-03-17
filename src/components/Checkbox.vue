<template>
  <div :class="['checkbox', { checked: checked }]"></div>
</template>

<script>
export default {
  props: {
    checked: Boolean,
  },
};
</script>

<style lang="scss">
$checked-color: #41b883;

.checkbox {
  display: flex;
  align-self: center;
  border: solid 2px $checked-color;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.2s;
  &:hover {
    background-color: rgba($checked-color, 0.1);
    transform: scale(1.1);
  }
}

.checkbox.checked {
  background-color: $checked-color;
  &:after {
    content: "";
    display: inline-block;
    transform: rotate(45deg) translate(-35%, 40%);
    height: 1rem;
    width: 1rem;
    margin-left: 60%;
    border-bottom: 5px solid white;
    border-right: 5px solid white;
  }
}
</style>
