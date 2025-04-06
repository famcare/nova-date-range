<template>
    <default-field :field="field">
        <template #field>
            <date-range-picker
                class="w-full form-control form-input form-input-bordered"
                mode="sa"
                :name="field.name"
                :field="field"
                :value="value"
                :seperator="seperator"
                :firstDayOfWeek="firstDayOfWeek"
                :dateFormat="format"
                :placeholder="placeholder"
                @change="handleChange"
                :disabled="isReadonly"
            />

            <p v-if="hasError" class="my-2 text-danger">
                {{ firstError }}
            </p>
        </template>
    </default-field>
</template>

<script>
import { defineComponent } from 'vue'
import DateRangePicker from './DateRangePicker'

// Create your own HandlesValidationErrors mixin
const HandlesValidationErrors = {
    computed: {
        hasError() {
            return this.errors && this.errors.has(this.field.attribute)
        },
        firstError() {
            return this.errors ? this.errors.first(this.field.attribute) : ''
        },
    }
}

export default defineComponent({
    name: 'DateRangeField',

    extends: FormField, // provided globally by Nova

    mixins: [HandlesValidationErrors],

    components: {
        DateRangePicker,
    },

    computed: {
        format() {
            return this.field.format
        },
        seperator() {
            return this.field.seperator
        },
        firstDayOfWeek() {
            return this.field.firstDayOfWeek || 0
        },
        placeholder() {
            return `${moment().format('YYYY-MM-DD')} ${this.field.seperator} ${moment().format('YYYY-MM-DD')}`
        }
    },
})
</script>
