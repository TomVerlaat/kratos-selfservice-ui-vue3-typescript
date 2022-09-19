<template lang="pug">
// Create a div with the ory-flow class
.ory-flow
  form(
    :id='formId'
    :action='flow.ui.action'
    :method='flow.ui.method'
  )
    // Render the OryUiNode vue component
    OryUiNode.ui-node(
      v-for='node in flow.ui.nodes'
      :key='getNodeId(node)'
      :id='getNodeId(node)'
      :node='node'
    )
  // Create a div with the messages class  
  .messages(v-if='flow.ui.messages')
    // Render the OryUIMessage component
    OryUiMessage(
      v-for='message in flow.ui.messages'
      :message='message'
    )
</template>

<script setup lang="ts">
import type {
  SelfServiceLoginFlow,
  SelfServiceRegistrationFlow,
  SelfServiceRecoveryFlow,
  SelfServiceSettingsFlow,
  SelfServiceVerificationFlow,
} from '@ory/client';
import OryUiNode from './OryUiNode.vue';
import OryUiMessage from './OryUiMessage.vue';
import { getNodeId } from '@ory/integrations/ui';

// Defines properties that should be inserted when calling this OryFlow component. 
defineProps<{
  flow:
    // Used in template to verify if properties exist
    | SelfServiceLoginFlow
    | SelfServiceRegistrationFlow
    | SelfServiceRecoveryFlow
    | SelfServiceSettingsFlow
    | SelfServiceVerificationFlow;
  formId?: string;
}>();
</script>

<style scoped lang="scss">
.ui-node + .ui-node {
  margin-top: var(--space-2);
}

.message {
  margin-top: var(--space-2);
}
</style>
