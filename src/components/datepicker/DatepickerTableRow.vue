<template>
    <div class="datepicker-row">
        <template v-for="(day, index) in week">
            <a v-if="selectableDate(day)"
                :key="index"
                :class="classObject(day)"
                class="datepicker-cell"
                role="button"
                tabindex="0"
                aria-label="Select Date"
                @click="emitChosenDate(day)"
                @keydown.enter="emitChosenDate(day)"
                @keydown.space.prevent="emitChosenDate(day)">
                {{ day.getDate() }}
            </a>
            <div v-else
                :key="index"
                :class="classObject(day)"
                class="datepicker-cell">
                {{ day.getDate() }}
            </div>
        </template>
    </div>
</template>

<script>
    export default {
        name: 'bDatepickerTableRow',
        props: {
            selectedDate: Date,
            week: {
                type: Array,
                required: true
            },
            month: {
                type: Number,
                required: true
            },
            minDate: Date,
            maxDate: Date
        },
        methods: {
            /*
            * Check that selected day is within earliest/latest params and
            * is within this month
            */
            selectableDate(day) {
                const validity = []

                if (this.minDate) {
                    validity.push(day >= this.minDate)
                }

                if (this.maxDate) {
                    validity.push(day <= this.maxDate)
                }

                validity.push(day.getMonth() === this.month)

                return !validity.includes(false)
            },

            /*
            * Emit select event with chosen date as payload
            */
            emitChosenDate(day) {
                if (this.selectableDate(day)) {
                    this.$emit('select', day)
                }
            },

            /*
            * Build classObject for cell using validations
            */
            classObject(day) {
                function dateMatch(dateOne, dateTwo) {
                    // if either date is null or undefined, return false
                    if (!dateOne || !dateTwo) {
                        return false
                    }

                    return (dateOne.getDate() === dateTwo.getDate() &&
                        dateOne.getFullYear() === dateTwo.getFullYear() &&
                        dateOne.getMonth() === dateTwo.getMonth())
                }

                return {
                    'is-selected': dateMatch(day, this.selectedDate),
                    'is-today': dateMatch(day, new Date()),
                    'is-selectable': this.selectableDate(day),
                    'is-unselectable': !this.selectableDate(day)
                }
            }
        }
    }
</script>
