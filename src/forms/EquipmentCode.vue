<script setup lang="ts">
import { useUserStore } from "@/stores/user";
import { computed, ref } from "vue";
import { useI18n } from "vue-i18n";
import BaseForm from "./BaseForm.vue";

const success = ref(false);

const baseForm = ref();

const emit = defineEmits(["success"]);

const { t } = useI18n();

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

const equipmentCodes = computed(() => [
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
    name: t("GBAS landing system"),
  },
  {
    code: "B",
    name: t("LPV (APV with SBAS)"),
  },
  {
    code: "C",
    name: t("LORAN C"),
  },
  {
    code: "D",
    name: t("DME"),
  },
  {
    code: "E1",
    name: t("FMC WPR ACARS"),
  },
  {
    code: "E2",
    name: t("D-FIS ACARS"),
  },
  {
    code: "E3",
    name: t("PDC ACARS"),
  },
  {
    code: "F",
    name: t("ADF"),
  },
  {
    code: "G",
    name: t(
      "GNSS (If the letter G is used, the types of external GNSS augmentation, if any, are specified in Item 18 following the indicator NAV/ and separated by a space.)"
    ),
  },
  {
    code: "H",
    name: t("HF RTF (HF RadioTelephone)"),
  },
  {
    code: "I",
    name: t("INS"),
  },
  {
    code: "J1",
    name: t("CPDLC ATN VDL Mode 2"),
  },
  {
    code: "J2",
    name: t("CPDLC FANS 1/A HFDL"),
  },
  {
    code: "J3",
    name: t("CPDLC FANS 1/A VDL Mode A/0"),
  },
  {
    code: "J4",
    name: t("CPDLC FANS 1/A VDL Mode 2"),
  },
  {
    code: "J5",
    name: t("CPDLC FANS 1/A SATCOM (INMARSAT)"),
  },
  {
    code: "J6",
    name: t("CPDLC FANS 1/A SATCOM (MTSAT)"),
  },
  {
    code: "J7",
    name: t("CPDLC FANS 1/A SATCOM (Iridium)"),
  },
  {
    code: "K",
    name: t("MLS"),
  },
  {
    code: "L",
    name: t("ILS"),
  },
  {
    code: "M1",
    name: t("ATC RTF SATCOM (INMARSAT)"),
  },
  {
    code: "M2",
    name: t("ATC RTF (MTSAT)"),
  },
  {
    code: "M3",
    name: t("ATC RTF (Iridium)"),
  },
  {
    code: "N",
    name: t("No COM/NAV equipment for the route carried or is unserviceable."),
  },
  {
    code: "O",
    name: t("VOR"),
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
    name: t(
      "PBN approved (If the letter R is used, the performance based navigation levels that can be met are specified in Item 18 following the indicator PBN/.)"
    ),
  },
  {
    code: "S",
    name: t(
      "Standard Equipment composed of VHF RTF, VOR and ILS, unless another combination is prescribed by the appropriate ATS authority."
    ),
  },
  {
    code: "T",
    name: t("TACAN"),
  },
  {
    code: "U",
    name: t("UHF RTF"),
  },
  {
    code: "V",
    name: t("VHF RTF"),
  },
  {
    code: "W",
    name: t("RVSM approved"),
  },
  {
    code: "X",
    name: t("MNPS approved"),
  },
  {
    code: "Y",
    name: t("Indicates 8.33 kHz radio band spacing (a standard requirement)"),
  },
  {
    code: "Z",
    name: t("Other equipment carried or other capabilities"),
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
]);

const templateAircraft = [
  {
    aircraftDeveloper: "Laminar Research",
    aircraftCode: "C172",
    code: "S",
  },
  {
    aircraftDeveloper: "Zibo",
    aircraftCode: "B738",
    code: "SDE2E3FGIJ1RWYZ",
  },
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

const decodeCodes = (code: string) => {
  //   Select the codes that are in the code
  selectedEquipmentCodes.value = equipmentCodes.value
    .filter((c) => code.includes(c.code))
    .map((c) => c.code);
};

const isDecoding = ref(false);

const saveCodeToLocalStorage = (name: string) => {
  localStorage.setItem("user-" + name, computedCode.value);
  saveName.value = "";
  getUserSavedCodes();
};

const userSavedCodes = ref([] as { name: string; code: string }[]);

const getUserSavedCodes = () => {
  const codes = [];
  for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);
    if (key && key.startsWith("user-")) {
      codes.push({
        name: key.replace("user-", ""),
        code: localStorage.getItem(key) || "",
      });
    }
  }
  userSavedCodes.value = codes;
  return codes;
};

const saveName = ref("");

getUserSavedCodes();
</script>

<template>
  <BaseForm
    ref="baseForm"
    @submit="submitForm"
    :disabled="success"
    :submit-text="$t('Send a new password')"
    :show-submit-button="false"
  >
    <!-- Dropdown of template aircraft -->
    <section>
      <h2 style="margin-bottom: 0">{{ $t("Select a template aircraft") }}</h2>
      <select @change="decodeCodes(($event.target as any).value)">
        <option value="">{{ $t("Select a template aircraft") }}</option>
        <option
          v-for="code in userSavedCodes"
          :key="code.name"
          :value="code.code"
        >
          {{ code.name }}
        </option>
        <option
          v-for="template in templateAircraft"
          :key="template.aircraftCode"
          :value="template.code"
        >
          {{ template.aircraftDeveloper }} {{ template.aircraftCode }}
        </option>
      </select>
    </section>

    <section v-if="isDecoding">
      <h2 style="margin-bottom: 0">{{ $t("Your equipment code") }}</h2>
      <!-- Input for existing code to checkbox -->
      <input
        type="text"
        @input="decodeCodes(($event.target as any).value)"
        :placeholder="$t('Equipment code')"
      />
      <a href="#" @click="isDecoding = false">{{ $t("Encode instead") }}</a>
    </section>

    <section v-else>
      <h2 style="margin-bottom: 0">{{ $t("Your generated ICAO code") }}</h2>
      <div>
        <code v-if="computedCode !== ''">{{ computedCode }}</code>
        <div v-else>
          {{
            $t(
              "Select an aircraft template or check some equipment below to see the generated code"
            )
          }}
        </div>
      </div>
      <a href="#" @click="isDecoding = true">{{ $t("Decode instead") }}</a>
    </section>

    <section>
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
    </section>

    <section>
      <h2>{{ $t("Save code") }}</h2>
      <input type="text" v-model="saveName" :placeholder="$t('Code name')" />
      <button @click="saveCodeToLocalStorage(saveName)">
        {{ $t("Save") }}
      </button>
    </section>
  </BaseForm>
</template>
