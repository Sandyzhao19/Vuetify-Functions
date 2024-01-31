<script setup lang="ts">
import { ref, watch } from "vue";
import { useRouter } from "vue-router";

const name = ref("");
const isFormDirty = ref(false);

watch([name], () => {
  isFormDirty.value = true;
});

const router = useRouter();

const onBeforeRouteLeave = (to: any, from: any, next: any) => {
  if (isFormDirty.value) {
    const confirmLeave = window.confirm(
      "You have unsaved changes. Are you sure you want to leave?"
    );
    if (confirmLeave) {
      isFormDirty.value = false;
      unwatch();
      next();
    } else {
      next(false);
    }
  } else {
    unwatch();
    next();
  }
};

const unwatch = router.afterEach(() => {
  onBeforeRouteLeave(router.currentRoute, router.currentRoute, () => {});
});
</script>

<template>
  <div>
    <form>
      <v-card variant="outlined">
        <div class="pa-5">
          <h4 class="text-h4 mt-1 text-strong">Name</h4>
        </div>
        <v-divider></v-divider>
        
        <v-card-text>
          <v-row>
            <v-col cols="12" lg="6">
              <v-row>
                <v-col cols="12">
                  <v-text-field
                    color="primary"
                    label="Title"
                    variant="outlined"
                    type="text"
                    hide-details
                    v-model="name"
                  >
                  </v-text-field>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </form>
  </div>
</template>
