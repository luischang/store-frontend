<template>
    <div class="q-pa-md row justify-center">
      <div style="width: 100%; max-width: 400px">
        <q-chat-message
          :text="['hey, how are you?']"
          sent
        />
        <q-chat-message
          :text="['doing fine, how r you?']"
        />
      </div>
    </div>
    <q-rating
        v-model="ratingModel"
        size="1.5em"
        icon="thumb_up"
        color="red-7"
      />
  </template>

<style>

</style>

<script>

</script>