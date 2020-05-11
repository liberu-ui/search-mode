<template>
    <core-search-mode v-bind="$attrs"
        v-on="$listeners">
        <template v-slot:default="{ clickEvents, query, value }">
            <span class="icon"
                v-if="query">
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
                        <template v-else-if="value === 'exactMatch'">
                            <falt :value="query[0]"
                                :transform="`shrink-2 ${query[2] ? 'left-10' : (!query[1] ? 'right-10' : '')}`"/>
                            <falt :value="query[1]"
                                :transform="`shrink-2 ${query[2] ? '' : 'right-10' }`"
                                v-if="query[1]"/>
                            <falt :value="query[2]"
                                transform="shrink-2 right-10"
                                v-if="query[2]"/>
                        </template>
                        <template v-else-if="value === 'doesntContain'">
                            <falt class="is-strikethrough" :value="query[0]"
                                :transform="`shrink-2 ${query[2] ? 'left-10' : (!query[1] ? 'right-10' : '')}`"/>
                            <falt class="is-strikethrough" :value="query[1]"
                                :transform="`shrink-2 ${query[2] ? '' : 'right-10' }`"
                                v-if="query[1]"/>
                            <falt class="is-strikethrough" :value="query[2]"
                                transform="shrink-2 right-10"
                                v-if="query[2]"/>
                        </template>
                        <template v-else-if="value === 'algolia'">
                            <fa :icon="['fab', 'algolia']"/>
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
import { faAlgolia } from '@fortawesome/free-brands-svg-icons';
import CoreSearchMode from '../renderless/CoreSearchMode.vue';

library.add(faAsterisk, faAlgolia);

export default {
    name: 'SearchMode',

    components: { CoreSearchMode },
};
</script>

<style lang="scss">
    .is-strikethrough {
        text-decoration: line-through;
    }
</style>
