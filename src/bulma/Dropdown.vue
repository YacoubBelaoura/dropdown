<template>
    <core-dropdown v-bind="$attrs"
        v-on="$listeners">
        <template v-slot:default="{
                triggerSelector, dropdownSelector, visible, open, close,
                opensUp, attemptClose, triggerEvents, dropdownEvents,
            }">
            <!-- <div class="dropdown is-active" -->
            <div class="dropdown is-active inline-flex relative block align-top"
                :class="{ 'is-up top-auto pb-1 pt-0': opensUp }"
                v-click-outside="close"
                v-on="dropdownEvents">
                <div class="dropdown-trigger"
                    :class="triggerSelector">
                    <slot name="trigger"
                        :triggerEvents="triggerEvents"
                        :open="open"
                        :visible="visible">
                        <!-- <button class="button input" -->
                        <button class="button input rounded text-center
                            whitespace-no-wrap m-0 select-none relative align-top
                            h-10 inline-flex rounded border border-gray-860
                            items-center max-w-full w-full bg-white focus:shadow-outline
                            focus:border-blue-500 active:border-blue-500  "
                            type="button"
                            v-on="triggerEvents">
                            <slot name="label"/>
                            <dropdown-indicator :open="visible"/>
                        </button>
                    </slot>
                </div>
                <fade>
                    <!-- <div class="dropdown-menu" -->
                    <div class="dropdown-menu block right-0 absolute top-full z-10 "
                        :class="dropdownSelector"
                        v-if="visible">
                        <!-- <div class="dropdown-content " -->
                        <div class="dropdown-content bg-white rounded shadow-md border border-gray-860 flex "
                            @click="attemptClose">
                            <slot name="controls"/>
                            <!-- <div class="options no-scrollbars"> -->
                            <div class="options no-scrollbars overflow-hidden">
                                <slot name="options"/>
                            </div>
                        </div>
                    </div>
                </fade>
            </div>
        </template>
    </core-dropdown>
</template>

<script>
import { clickOutside } from '@enso-ui/directives';
import { Fade } from '@enso-ui/transitions';
import DropdownIndicator from '@enso-ui/dropdown-indicator';
import CoreDropdown from '../renderless/CoreDropdown.vue';

export default {
    name: 'Dropdown',

    directives: { clickOutside },

    components: { CoreDropdown, Fade, DropdownIndicator },

    data: () => ({
        opensTop: false,
    }),
};
</script>

<style lang="scss">

    .dropdown {
        .dropdown-trigger {
            .button.input {
                @apply outline-none;
                min-width: 4em;
                justify-content: flex-start;
                line-height: 1.5;
                padding-bottom: calc(0.375em - 1px);
                padding-left: calc(0.625em - 1px);
                padding-right: calc(0.625em - 1px);
                padding-top: calc(0.375em - 1px);

                .angle {
                    position: absolute;
                    // top: 0.33rem;
                    [dir='ltr'] & {
                        right: 0.125rem;
                    }
                    [dir='rtl'] & {
                        left: 0.125rem;
                    }
                }
            }
        }

        .dropdown-content {
            width: fit-content;
            .options {
                width: inherit;
            }
        }
    }

</style>
