<template>
    <tab
        :label="title"
        :item-header-class="tabClass"
    >
        <div class="row g-3">
            <form-group-field
                id="form_config_api_secret"
                class="col-md-6"
                :field="v$.config.api_secret"
                :label="$gettext('Measurement Protocol API Secret')"
                :description="$gettext('This can be generated in the &quot;Events&quot; section for a measurement.')"
            />

            <form-group-field
                id="form_config_measurement_id"
                class="col-md-6"
                :field="v$.config.measurement_id"
                :label="$gettext('Measurement ID')"
                :description="$gettext('A unique identifier (i.e. &quot;G-A1B2C3D4&quot;) for this measurement stream.')"
            />
        </div>
    </tab>
</template>

<script setup lang="ts">
import FormGroupField from "~/components/Form/FormGroupField.vue";
import {useVuelidateOnFormTab} from "~/functions/useVuelidateOnFormTab";
import {required} from "@vuelidate/validators";
import Tab from "~/components/Common/Tab.vue";
import {WebhookComponentProps} from "~/components/Stations/Webhooks/EditModal.vue";
import {ApiGenericForm} from "~/entities/ApiInterfaces.ts";

defineProps<WebhookComponentProps>();

const form = defineModel<ApiGenericForm>('form', {required: true});

const {v$, tabClass} = useVuelidateOnFormTab(
    form,
    {
        config: {
            api_secret: {required},
            measurement_id: {required}
        }
    },
    () => ({
        config: {
            api_secret: '',
            measurement_id: ''
        }
    })
);
</script>
