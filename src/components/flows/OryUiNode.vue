<template lang="pug">
// Creates a div with the ory flow class
.ory-ui-node
  // Renders the OryUiNode Vue component
  OryUiNodeInput(
    v-if='isUiNodeInputAttributes(node.attributes)'
    :attributes='node.attributes'
    :meta='node.meta'
    :id='id'
  )
  p(v-if='isUiNodeAnchorAttributes(node.attributes)') Sample Text
  p(v-else-if='isUiNodeAnchorAttributes(node.attributes)') Anchor
  p(v-else-if='isUiNodeImageAttributes(node.attributes)') Image
  p(v-else-if='isUiNodeScriptAttributes(node.attributes)') Script
  p(v-else-if='isUiNodeTextAttributes(node.attributes)') Text
  button(
    v-else-if='node.type === "submit"'
    type='submit'
  )
  .messages(v-if='node.messages')
    OryUiMessage(
      v-for='message in node.messages'
      :message='message'
    )
</template>

<script setup lang="ts">
  import type { UiNode } from '@ory/client';
  import {
    isUiNodeAnchorAttributes,
    isUiNodeImageAttributes,
    isUiNodeInputAttributes,
    isUiNodeScriptAttributes,
    isUiNodeTextAttributes,
  } from '@ory/integrations/ui';
  import OryUiNodeInput from './OryUiNodeInput.vue';
  import OryUiMessage from './OryUiMessage.vue';
  
  defineProps<{
    node: UiNode;
    id: string;
  }>();
  </script>
