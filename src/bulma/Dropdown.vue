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
                <div class="dropdown-trigger w-full"
                    :class="triggerSelector">
                    <slot name="trigger"
                        :triggerEvents="triggerEvents"
                        :open="open"
                        :visible="visible">
                        <!-- <button class="button input" -->
                        <button class="button input focus:border-blue-500 focus:shadow-outline h-9  hover:shadow-inner hover:border-blue-300 w-full"
                            type="button"
                            v-on="triggerEvents">
                            <slot name="label"/>
                            <dropdown-indicator :open="visible"/>
                        </button>
                    </slot>
                </div>
                <fade>
                    <!-- <div class="dropdown-menu" -->
                    <div class="dropdown-menu block pt-1 right-0 absolute top-full z-10 "
                        :class="dropdownSelector"
                        v-if="visible">
                        <!-- <div class="dropdown-content " -->
                        <div class=" bg-white rounded-lg shadow-md border border-gray-860 flex py-2 flex-col overflow-y-auto"
                            @click="attemptClose">
                            <slot name="controls"/>
                            <!-- <div class="options no-scrollbars"> -->
                            <!-- <div class="options no-scrollbars overflow-hidden w-full "> -->
                            <div class="options no-scrollbars w-full overflow-y-auto max-h-20 ">
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
                @apply outline-none justify-between;
                min-width: 4rem;
                // justify-content: flex-start;
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
