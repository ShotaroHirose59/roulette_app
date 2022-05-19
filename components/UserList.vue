<template>
  <div>
    <span class="mr-2">{{ statusWord }}:</span>
    <span v-for="user in users" :key="user">{{ user }}, </span>
  </div>
</template>

<script>
export default {
  props: {
    statusWord: {
      type: String,
      required: true
    },
    users: {
      type: Array,
      required: true
    }
  },
}
</script>
