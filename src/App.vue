<script setup lang="ts">
import { ref } from 'vue'
import { useRegisterSW } from 'virtual:pwa-register/vue'

import ReloadPrompt from '@/components/ReloadPrompt.vue'

const serviceTitle = 'Service'
const serviceDescription = 'Description du service'
const logoText = ['Ministère', 'de l’intérieur']

const quickLinks = [
  {
    label: 'Home',
    path: '/',
    icon: 'ri-home-4-line',
    iconAttrs: { color: 'var(--red-marianne-425-625)' },
  },
  {
    label: 'À propos',
    path: '/a-propos',
    class: 'fr-fi-user-line',
  },
]
const searchQuery = ref('')

const {
  offlineReady,
  needRefresh,
  updateServiceWorker,
} = useRegisterSW()

const close = () => {
  offlineReady.value = false
  needRefresh.value = false
}

const inputLabelVisible = ref()
const inputLabelInvisible = ref()
const inputLabelVisibleOrInvisible = ref()
const visibleOrNot = ref(true)
</script>

<template>
  <DsfrHeader
    v-model="searchQuery"
    :service-title="serviceTitle"
    :service-description="serviceDescription"
    :logo-text="logoText"
    :quick-links="quickLinks"
    show-search
  />
  <div class="fr-container">
    <fieldset class="fr-my-4w  fr-p-2w">
      <legend class="fr-px-2v">
        DsfrInput avec label visible
      </legend>
      <DsfrInput
        v-model="inputLabelVisible"
        type="inputType"
        label="Label visible"
        label-visible
        placeholder="Input avec label visible"
      />
    </fieldset>
    <fieldset class="fr-my-4w  fr-p-2w">
      <legend class="fr-px-2v">
        DsfrInput avec label invisible
      </legend>
      <DsfrInput
        v-model="inputLabelInvisible"
        type="inputType"
        label="Label invisible"
        :label-visible="false"
        placeholder="Input avec label invisible"
      />
    </fieldset>
    <fieldset class="fr-my-4w  fr-p-2w">
      <legend class="fr-px-2v">
        DsfrInput avec label visible ou invisible
      </legend>
      <DsfrToggleSwitch
        v-model="visibleOrNot"
        label="Rendre le label visible"
      />
      <DsfrInput
        v-model="inputLabelVisibleOrInvisible"
        type="inputType"
        label="Label visible ou invisible"
        :label-visible="visibleOrNot"
        placeholder="Input avec label à visibilité dynamique"
      />
    </fieldset>

    <div class="flex flex-column h-full">
      <p>
        <a
          class="fr-link"
          type="button"
          icon="ri-github-fill"
          href="https://github.com/laruiss/dsfr-input-label-example"
        >
          Aller au code source
          <VIcon name="ri-github-fill" />
        </a>
      </p>
    </div>
  </div>

  <ReloadPrompt
    :offline-ready="offlineReady"
    :need-refresh="needRefresh"
    @close="close()"
    @update-service-worker="updateServiceWorker()"
  />
</template>
