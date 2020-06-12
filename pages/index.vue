<template>
  <div>
    <validation-observer ref="observer" v-slot="{ valid }">
      <label for="email">Email</label>
      <validation-provider
        v-slot="{ errors }"
        rules="required"
        name="email"
      >
        <input
            ref="email"
            v-model="email"
            field="email"
            name="Email"
          />
        <div
          v-if="errors.length"
        >
          {{ errors[0] }}
        </div>
      </validation-provider>
      <label for="password">Password</label>
      <validation-provider
        v-slot="{ errors }"
        rules="required"
        name="password"
      >
        <input
          v-model="password"
          name="password"
          type="password"
        />
        <div
          v-if="errors.length"
        >
          {{ errors[0] }}
        </div>
      </validation-provider>
      <button
        :disabled="!valid"
        @click="login"
      >
        Validate
      </button>
    </validation-observer>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { ValidationProvider, ValidationObserver } from 'vee-validate'
export default Vue.extend({
  components: {
    ValidationProvider,
    ValidationObserver
  },
  data() {
    return {
      eye: true as boolean,
      email: '' as string,
      password: '' as string,
    }
  },
  methods: {
    async login() {
      const isValid = await (this.$refs.observer as any).validate()
      if (isValid) {
        alert('valid')
      }
      else alert('invalid')
    }
  }
})
</script>
