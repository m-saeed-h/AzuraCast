<template>
    <tr>
        <td>
            <form-group-field
                :id="'form_edit_title_'+index"
                :field="v$.title"
            />
        </td>
        <td>
            <form-group-field
                :id="'form_edit_publish_at_'+index"
                :field="v$.publish_at"
            >
                <template #default="{id, model, fieldClass}">
                    <publish-at-fields
                        :id="id"
                        v-model="model.$model"
                        :class="fieldClass"
                    />
                </template>
            </form-group-field>
        </td>
        <td>
            <form-group-checkbox
                :id="'form_edit_explicit_'+index"
                :field="v$.explicit"
            />
        </td>
        <td>
            <form-group-field
                :id="'form_edit_season_number_'+index"
                :field="v$.season_number"
                input-type="number"
                :input-attrs="{ step: '1' }"
                clearable
            />
        </td>
        <td>
            <form-group-field
                :id="'form_edit_episode_number_'+index"
                :field="v$.episode_number"
                input-type="number"
                :input-attrs="{ step: '1' }"
                clearable
            />
        </td>
    </tr>
</template>

<script setup lang="ts">
import {required} from "@vuelidate/validators";
import useVuelidate from "@vuelidate/core";
import FormGroupField from "~/components/Form/FormGroupField.vue";
import FormGroupCheckbox from "~/components/Form/FormGroupCheckbox.vue";
import PublishAtFields from "~/components/Stations/Podcasts/Common/PublishAtFields.vue";
import {ApiPodcastEpisode} from "~/entities/ApiInterfaces.ts";

type T = Partial<ApiPodcastEpisode>;

defineProps<{
    index: number,
}>();

const row = defineModel<T>('row');

const v$ = useVuelidate<T>(
    {
        id: {required},
        title: {required},
        publish_at: {},
        explicit: {},
        season_number: {},
        episode_number: {}
    },
    row
);
</script>
