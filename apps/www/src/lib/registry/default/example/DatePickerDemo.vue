<script setup lang="ts">
import { ref } from 'vue'
import {
  DateFormatter,
  type DateValue,
  getLocalTimeZone,
  CalendarDate
} from '@internationalized/date'
import { toDate } from 'radix-vue/date'

import { Calendar as CalendarIcon } from 'lucide-vue-next'
import { Calendar } from '@/lib/registry/default/ui/calendar'
import { Button } from '@/lib/registry/default/ui/button'
import { Popover, PopoverContent, PopoverTrigger } from '@/lib/registry/default/ui/popover'
import { cn } from '@/lib/utils'

const df = new DateFormatter('en-US', {
  dateStyle: 'long',
})

const value = ref<DateValue>(new CalendarDate(2022, 2, 3))
</script>

<template>
  <Popover>
    <PopoverTrigger as-child>
      <Button
        variant="outline"
        :class="cn(
          'w-[280px] justify-start text-left font-normal',
          !value && 'text-muted-foreground',
        )"
      >
        <CalendarIcon class="mr-2 h-4 w-4" />
        {{ value ? df.format(toDate(value.value)) : "Pick a date" }}
      </Button>
    </PopoverTrigger>
    <PopoverContent class="w-auto p-0">
      <Calendar v-model="value" initial-focus />
    </PopoverContent>
  </Popover>
</template>
