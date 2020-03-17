<template>
    <core-search-mode v-bind="$attrs"
        v-on="$listeners">
        <template v-slot:default="{ clickEvents, query, value }"
            v-if="query">
            <span class="icon">
                <a class="is-naked"
                    v-on="clickEvents">
                    <fal :key="query">
                        <template v-if="value === 'startsWith'">
                            <falt :value="query[0]"
                                :transform="`shrink-2 ${query[1] ? 'left-10' : '' }`"/>
                            <falt :value="query[1]"
                                transform="shrink-2"
                                v-if="query[1]"/>
                            <fa icon="asterisk" transform="shrink-6 right-10"/>
                        </template>
                        <template v-else-if="value === 'full'">
                            <fa icon="asterisk" transform="shrink-6 left-10"/>
                            <falt :value="query[0]" transform="shrink-2"/>
                            <fa icon="asterisk" transform="shrink-6 right-10"/>
                        </template>
                        <template v-else-if="value === 'endsWith'">
                            <fa icon="asterisk"
                                :transform="`shrink-6 ${query[1] ? 'left-10' : '' }`"/>
                            <falt :value="query[0]"
                                :transform="`shrink-2 ${query[1] ? '' : 'right-10' }`"/>
                            <falt :value="query[1]"
                                transform="shrink-2 right-10"
                                v-if="query[1]"/>
                        </template>
                    </fal>
                </a>
            </span>
        </template>
    </core-search-mode>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faAsterisk } from '@fortawesome/free-solid-svg-icons';
import CoreSearchMode from '../renderless/CoreSearchMode.vue';

library.add(faAsterisk);

export default {
    name: 'SearchMode',

    components: { CoreSearchMode },
};
</script>
