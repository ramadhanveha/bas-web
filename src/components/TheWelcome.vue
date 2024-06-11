<template>
  <v-sheet class="mx-auto" width="300">
    <v-form enable>
      <div>
        <label for="Username">Username</label>
      <v-text-field
        v-model="firstName"
        label="First name"
      ></v-text-field>
    </div>
    <div>
        <label for="Password">Password</label>
      <v-text-field
        v-model="firstName"
        label="First name"
      ></v-text-field>
    </div>
    </v-form>
  </v-sheet>
</template>
<script>
  export default {
    data: () => ({
      firstName: '',
      lastName: '',
    }),
  }
</script>