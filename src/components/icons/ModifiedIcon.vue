<template>
  <div
    v-if="dataChanged"
    class="float-right"
    :title="message"
  >
    <FontAwesomeIcon
      size="lg"
      icon="exclamation-circle"
      :style="{ color: '#FF8200' }"
    />
  </div>
</template>

<script>
/*
 * Creates an icon with a warning if a variable has changed in value as compared
 * to a comparison object. The icon is floated to the right and will display the
 * specified message if you hover over it.
 *
 */

import { isEqual } from 'lodash';

// Use icons from Font Awesome.
import { library } from '@fortawesome/fontawesome-svg-core';
import {
  faExclamationCircle,
} from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

// Set up exclamation circle for FontAwesome.
library.add(faExclamationCircle);

export default {
  name: 'ModifiedIcon',
  components: {
    FontAwesomeIcon,
  },
  props: {
    message: {
      type: String,
      default: 'This element has changed! Please remember to save it.',
    },
    compare: Object, /* Object to check for changes. */
    compareTo: Object, /* Changes will be determined by comparing this to this.compare */
  },
  computed: {
    dataChanged() { return !isEqual(this.compare, this.compareTo); },
  },
};
</script>
