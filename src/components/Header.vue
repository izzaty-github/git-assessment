<template>
    <div>
        <h1 class="text-center">{{ title }}</h1>
    </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
      title: String
}
}
</script>
