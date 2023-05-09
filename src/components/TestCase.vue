<script lang="ts">
import { ref, defineComponent } from "vue";
import type { VForm } from "vuetify/components";

export default defineComponent({
  setup() {
    const requiredRules = [(msg: string) => !!msg || "This field is required"];
    const name = ref("");
    const myRef = ref<VForm | null>(null);
    const isValid = ref(false);
    async function validate() {
      if (myRef.value) {
        const { valid } = await myRef.value.validate();
        isValid.value = valid;
      }
    }
    return {
      requiredRules,
      name,
      myRef,
      isValid,
      validate,
    };
  },
});
</script>
<template>
  <v-form ref="myRef">
    <v-text-field v-model="name" label="Name" required :rules="requiredRules" />
    <v-btn @click="validate">Validate</v-btn>
    Form is {{ isValid ? "Valid" : "Invalid" }}
  </v-form>
</template>
