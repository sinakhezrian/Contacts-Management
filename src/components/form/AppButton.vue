<template>
  <button :type="type" :class="['app-btn', buttonType]" @click="handleClick">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "AppButton",
  props: {
    text: {
      type: String,
      required: true,
    },
    buttonType: {
      type: String,
      primary: 'primary',
      danger: 'danger',
      warning: 'primary',
      outline: 'outline',
    },
    type: {
      type: String,
      button: "button",
      submit: "submit"
    },
    onClick: {
      type: Function,
      default: () => { },
    },
  },
  methods: {
    handleClick() {
      this.onClick();
    },
  },
};
</script>

<style scoped>
.app-btn {
  --danger: #d00000;
  --primary: #023e7d;
  --warning: #faa307;

  border: 0;
  color: #fff;
  padding: 6px 12px;
  border-radius: 5px;
  min-height: 36px;
  margin-inline: 4px;
}

.app-btn.outline {
  background: transparent !important;
  color: var(--primary) !important;
  outline: 1px solid var(--primary);
}

.app-btn.app-btn:not(.outline):focus {
  outline: unset;
}

.app-btn.primary {
  background: var(--primary);
  outline: var(--primary);
}

.app-btn.danger {
  background: var(--danger);
  outline: var(--danger);
}

.app-btn.warning {
  background: var(--warning);
  outline: var(--warning);
}
</style>