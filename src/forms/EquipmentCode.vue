<script setup lang="ts">
import { useUserStore } from "@/stores/user";
import { computed, ref } from "vue";
import BaseForm from "./BaseForm.vue";

const success = ref(false);

const baseForm = ref();

const emit = defineEmits(["success"]);

const userStore = useUserStore();
// The submit function. If there is just the email, check if the email is valid. If it is not, set the register mode. If it is, set the login mode.
const submitForm = async () => {
  if (!userStore.userEmail) {
    return;
  }
  const response = await userStore.sendPasswordResetEmail(userStore.userEmail);
  if (response === true) {
    success.value = response;
    emit("success");
  } else if (typeof response === "object") {
    baseForm.value.setInputErrors(response.data.errors);
  }
  return success.value;
};

const equipmentCodes = [
  // Radio communication, navigation and approach aid equipment and capabilities[edit] -->
  // A GBAS landing system
  // B LPV (APV with SBAS)
  // C LORAN C
  // D DME
  // E1 FMC WPR ACARS
  // E2 D-FIS ACARS
  // E3 PDC ACARS
  // F ADF
  // G GNSS (If the letter G is used, the types of external GNSS augmentation, if any, are specified in Item 18 following the indicator NAV/ and separated by a space.)
  // H HF RTF (HF RadioTelephone)
  // I INS
  // J1 CPDLC ATN VDL Mode 2
  // J2 CPDLC FANS 1/A HFDL
  // J3 CPDLC FANS 1/A VDL Mode A/0
  // J4 CPDLC FANS 1/A VDL Mode 2
  // J5 CPDLC FANS 1/A SATCOM (INMARSAT)
  // J6 CPDLC FANS 1/A SATCOM (MTSAT)
  // J7 CPDLC FANS 1/A SATCOM (Iridium)
  // K MLS
  // L ILS
  // M1 ATC RTF SATCOM (INMARSAT)
  // M2 ATC RTF (MTSAT)
  // M3 ATC RTF (Iridium)
  // N No COM/NAV equipment for the route carried or is unserviceable.
  // O VOR
  // P1-P9 Reserved for RCP
  // Q (Not allocated)
  // R PBN approved (If the letter R is used, the performance based navigation levels that can be met are specified in Item 18 following the indicator PBN/.)
  // S Standard Equipment composed of VHF RTF, VOR and ILS, unless another combination is prescribed by the appropriate ATS authority.
  // T TACAN
  // U UHF RTF
  // V VHF RTF
  // W RVSM approved
  // X MNPS approved
  // Y Indicates 8.33 kHz radio band spacing (a standard requirement)
  // Z Other equipment carried or other capabilities
  {
    code: "A",
    name: "GBAS landing system",
  },
  {
    code: "B",
    name: "LPV (APV with SBAS)",
  },
  {
    code: "C",
    name: "LORAN C",
  },
  {
    code: "D",
    name: "DME",
  },
  {
    code: "E1",
    name: "FMC WPR ACARS",
  },
  {
    code: "E2",
    name: "D-FIS ACARS",
  },
  {
    code: "E3",
    name: "PDC ACARS",
  },
  {
    code: "F",
    name: "ADF",
  },
  {
    code: "G",
    name: "GNSS (If the letter G is used, the types of external GNSS augmentation, if any, are specified in Item 18 following the indicator NAV/ and separated by a space.)",
  },
  {
    code: "H",
    name: "HF RTF (HF RadioTelephone)",
  },
  {
    code: "I",
    name: "INS",
  },
  {
    code: "J1",
    name: "CPDLC ATN VDL Mode 2",
  },
  {
    code: "J2",
    name: "CPDLC FANS 1/A HFDL",
  },
  {
    code: "J3",
    name: "CPDLC FANS 1/A VDL Mode A/0",
  },
  {
    code: "J4",
    name: "CPDLC FANS 1/A VDL Mode 2",
  },
  {
    code: "J5",
    name: "CPDLC FANS 1/A SATCOM (INMARSAT)",
  },
  {
    code: "J6",
    name: "CPDLC FANS 1/A SATCOM (MTSAT)",
  },
  {
    code: "J7",
    name: "CPDLC FANS 1/A SATCOM (Iridium)",
  },
  {
    code: "K",
    name: "MLS",
  },
  {
    code: "L",
    name: "ILS",
  },
  {
    code: "M1",
    name: "ATC RTF SATCOM (INMARSAT)",
  },
  {
    code: "M2",
    name: "ATC RTF (MTSAT)",
  },
  {
    code: "M3",
    name: "ATC RTF (Iridium)",
  },
  {
    code: "N",
    name: "No COM/NAV equipment for the route carried or is unserviceable.",
  },
  {
    code: "O",
    name: "VOR",
  },
  //   {
  //     code: "P1",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P2",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P3",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P4",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P5",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P6",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P7",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P8",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "P9",
  //     name: "Reserved for RCP",
  //   },
  //   {
  //     code: "Q",
  //     name: "Not allocated",
  //   },
  {
    code: "R",
    name: "PBN approved (If the letter R is used, the performance based navigation levels that can be met are specified in Item 18 following the indicator PBN/.)",
  },
  {
    code: "S",
    name: "Standard Equipment composed of VHF RTF, VOR and ILS, unless another combination is prescribed by the appropriate ATS authority.",
  },
  {
    code: "T",
    name: "TACAN",
  },
  {
    code: "U",
    name: "UHF RTF",
  },
  {
    code: "V",
    name: "VHF RTF",
  },
  {
    code: "W",
    name: "RVSM approved",
  },
  {
    code: "X",
    name: "MNPS approved",
  },
  {
    code: "Y",
    name: "Indicates 8.33 kHz radio band spacing (a standard requirement)",
  },
  {
    code: "Z",
    name: "Other equipment carried or other capabilities",
  },
  // Surveillance equipment codes[edit]
  // SSR (secondary surveillance radar)[edit]
  // N No surveillance equipment for the route to be flown is carried, or the equipment is unserviceable
  // A Transponder – Mode A (4 digits – 4,096 codes)
  // C Transponder – Mode A (4 digits – 4,096 codes) and Mode C
  // E Transponder — Mode S, including aircraft identification, pressure-altitude and extended squitter (ADS-B) capability
  // H Transponder — Mode S, including aircraft identification, pressure-altitude and enhanced surveillance capability
  // I Transponder — Mode S, including aircraft identification, but no pressure-altitude capability
  // L Transponder — Mode S, including aircraft identification, pressure-altitude, extended squitter (ADS-B) and enhanced surveillance capability
  // P Transponder — Mode S, including pressure-altitude, but no aircraft identification capability
  // S Transponder — Mode S, including both pressure altitude and aircraft identification capability
  // X Transponder — Mode S with neither aircraft identification nor pressure-altitude capability
  // ADS-B[edit]
  // B1 ADS-B with dedicated 1090 MHz ADS-B “out” capability
  // B2 ADS-B with dedicated 1090 MHz ADS-B “out” and “in” capability
  // U1 ADS-B “out” capability using UAT
  // U2 ADS-B “out” and “in” capability using UAT
  // V1 ADS-B “out” capability using VDL Mode 4
  // V2 ADS-B “out” and “in” capability using VDL Mode 4
  // ADS-C[edit]
  // D1 ADS-C with FANS 1/A capabilities
  // G1 ADS-C with ATN capabilities
  //   {
  //     code: "SSR",
  //     name: "Secondary Surveillance Radar",
  //   },
  //   {
  //     code: "N",
  //     name: "No COM/NAV equipment for the route carried or is unserviceable.",
  //   },
  //   {
  //     code: "A Transponder",
  //     name: "ADS-B with dedicated 1090 MHz ADS-B “out” capability",
  //   },
];

const selectedEquipmentCodes = ref([] as string[]);

// The codes must be in alphabetical order
const computedCode = computed(() => {
  const codes = selectedEquipmentCodes.value;
  codes.sort();
  //   It must be alphabetical order, but if there is the "S" code, it must be the first one
  if (codes.includes("S")) {
    codes.splice(codes.indexOf("S"), 1);
    codes.unshift("S");
  }
  return codes.join("");
});
</script>

<template>
  <BaseForm
    ref="baseForm"
    @submit="submitForm"
    :disabled="success"
    :submit-text="$t('Send a new password')"
    :show-submit-button="false"
  >
    <h2 style="margin-bottom: 0">{{ $t("Select your equipment") }}</h2>
    <!-- For each equipment code, create a label and checkbox -->
    <template v-for="code in equipmentCodes" :key="code.code">
      <label :for="code.code">
        <input
          type="checkbox"
          :id="code.code"
          :value="code.code"
          v-model="selectedEquipmentCodes"
        />
        {{ code.name }}
      </label>
    </template>
  </BaseForm>
  <hr />
  <h2 style="margin-bottom: 0">{{ $t("Your generated code") }}</h2>
  <code>{{ computedCode }}</code>
</template>