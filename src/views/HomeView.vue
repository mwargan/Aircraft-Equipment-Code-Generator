<script setup lang="ts">
import EquipmentCode from "@/forms/EquipmentCode.vue";
</script>

<template>
  <main>
    <h1 style="margin-bottom: 0">{{ $t("ICAO Equipment Code Generator") }}</h1>
    <p>
      {{ $t("Generate an ICAO equipment code for use on VATSIM flightplans!") }}
    </p>
    <EquipmentCode />
  </main>
</template>
