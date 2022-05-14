<template>
  <div
    id="liveToast"
    :class="[
      'toast',
      'position-fixed',
      'top-0',
      'start-50',
      'translate-middle-x',
      'text-white',
      'bg-success',
      'border-0',
    ]"
    role="alert"
    aria-live="assertive"
    aria-atomic="true"
    style="position: absolute; width: auto; text-align: center"
  >
    <div :class="[messageStyle, 'd-flex']">
      <div class="toast-body">{{ message }}</div>
      <button
        type="button"
        class="btn-close btn-close-white me-2 m-auto"
        data-bs-dismiss="toast"
        aria-label="Close"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Toast",
  props: {
    message: {
      type: String,
      default: "",
    },
    messageStyle: {
      type: String,
      default: "bg-warning",
    },
  },
};
</script>

<style>
</style>