<script setup lang="ts">
import {ref, computed} from "vue";

const allDay = ref(false);
const showStartTimePickerDialog = ref<boolean>(false);
const showEndTimePickerDialog = ref<boolean>(false);

const startDatetime = ref(new Date());
const startDate = ref(new Date());
const endDatetime = ref(new Date());
const endDate = ref(new Date());

const formattedStartDatetime = computed(() => {
  return startDatetime.value.toLocaleDateString('en-US', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',

    hour: 'numeric',
    minute: 'numeric',
    hour12: true,
  });
});

const formattedStartDate = computed(() => {
  return startDate.value.toLocaleDateString('en-US', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  });
});

const formattedEndDatetime = computed(() => {
  return endDatetime.value.toLocaleDateString('en-US', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',

    hour: 'numeric',
    minute: 'numeric',
    hour12: true,
  });
});

const formattedEndDate = computed(() => {
  return endDate.value.toLocaleDateString('en-US', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  });
});
</script>

<template>
  <form>
    <v-card variant="outlined">
      <div class="pa-5">
        <h5 class="text-subtitle-1 mt-1">Event Detail</h5>
      </div>

      <v-divider></v-divider>
      <v-card-text>
        <v-row>
          <v-col cols="12">
            <v-switch
              color="primary"
              v-model="allDay"
              hide-details
              label="All day"
            ></v-switch>
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12" lg="6">
            <v-text-field
              v-if="!allDay"
              v-model="formattedStartDatetime"
              label="Start Time"
              color="primary"
              variant="outlined"
              append-inner-icon="mdi-calendar-range"
              @mousedown:control="showStartTimePickerDialog = true"
            >
            </v-text-field>

            <v-text-field
              v-if="allDay"
              v-model="formattedStartDate"
              label="Start Date"
              color="primary"
              variant="outlined"
              append-inner-icon="mdi-calendar-range"
              @mousedown:control="showStartTimePickerDialog = true"
            >
            </v-text-field>

            <v-dialog v-model="showStartTimePickerDialog" width="auto">
              <v-card>
                <v-card-text>
                  <v-date-picker
                    v-if="!allDay"
                    v-model="startDatetime"
                    mode="dateTime"
                  />
                  <v-date-picker
                    v-if="allDay"
                    v-model="startDate"
                    mode="date"
                  />

                  <div
                    class="mt-5"
                    style="display: flex; justify-content: flex-end"
                  >
                    <v-btn
                      color="primary"
                      variant="text"
                      @click="showStartTimePickerDialog = false"
                      >Cancel
                    </v-btn>
                    <v-btn
                      color="primary"
                      variant="text"
                      @click="showStartTimePickerDialog = false"
                      >OK</v-btn
                    >
                  </div>
                </v-card-text>
              </v-card>
            </v-dialog>
          </v-col>

          <v-col cols="12" lg="6">
            <v-text-field
              v-if="!allDay"
              v-model="formattedEndDatetime"
              label="End Time"
              color="primary"
              variant="outlined"
              append-inner-icon="mdi-calendar-range"
              @mousedown:control="showEndTimePickerDialog = true"
            >
            </v-text-field>

            <v-text-field
              v-if="allDay"
              v-model="formattedEndDate"
              label="End Date"
              color="primary"
              variant="outlined"
              append-inner-icon="mdi-calendar-range"
              @mousedown:control="showEndTimePickerDialog = true"
            >
            </v-text-field>

            <v-dialog v-model="showEndTimePickerDialog" width="auto">
              <v-card>
                <v-card-text>
                  <v-date-picker
                    v-if="!allDay"
                    v-model="endDatetime"
                    mode="dateTime"
                  />
                  <v-date-picker v-if="allDay" v-model="endDate" mode="date" />

                  <div
                    class="mt-5"
                    style="display: flex; justify-content: flex-end"
                  >
                    <v-btn
                      color="primary"
                      variant="text"
                      @click="showEndTimePickerDialog = false"
                      >Cancel
                    </v-btn>
                    <v-btn
                      color="primary"
                      variant="text"
                      @click="showEndTimePickerDialog = false"
                      >OK</v-btn
                    >
                  </div>
                </v-card-text>
              </v-card>
            </v-dialog>
          </v-col>
        </v-row>

      </v-card-text>
    </v-card>
  </form>
</template>
