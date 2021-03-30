<template>
  <div class="bg-red-500 text-white p-3 mb-4 rounded">
    {{ pesan }}
  </div>
</template>
<script>
export default {
  name: 'Notification',
  props: ['pesan'],
}
</script>
