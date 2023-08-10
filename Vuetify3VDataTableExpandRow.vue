<script setup lang = "ts" >
import { VDataTable } from 'vuetify/labs/VDataTable'

interface Dessert {
    id: number;
    name: string;
    calories: number;
    fat: number;
    carbs: number;
    protein: number;
    iron: string;
}

interface Header {
    title: string;
    value: string;
    align: string;
    sortable: boolean;
}

const headers: Header[] = [
    { title: 'Dessert (100g serving)', value: 'name', align: 'start', sortable: false },
    { title: 'Calories', value: 'calories', align: 'start', sortable: false },
    { title: 'Fat (g)', value: 'fat', align: 'start', sortable: false },
    { title: 'Carbs (g)', value: 'carbs', align: 'start', sortable: false },
    { title: 'Protein (g)', value: 'protein', align: 'start', sortable: false },
    { title: 'Iron (%)', value: 'iron', align: 'start', sortable: false }
];

const desserts: Dessert[] = [
    {
        id: 0,
        name: 'Frozen Yogurt',
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        iron: '1%',
    },
    {
        id: 1,
        name: 'Frozen Yogurt',
        calories: 237,
        fat: 9.0,
        carbs: 37,
        protein: 4.3,
        iron: '1%',
    },
    {
        id: 2,
        name: 'Eclair',
        calories: 262,
        fat: 16.0,
        carbs: 23,
        protein: 6.0,
        iron: '7%',
    },
    {
        id: 3,
        name: 'Cupcake',
        calories: 305,
        fat: 3.7,
        carbs: 67,
        protein: 4.3,
        iron: '8%',
    },
    {
        id: 3,
        name: 'Gingerbread',
        calories: 356,
        fat: 16.0,
        carbs: 49,
        protein: 3.9,
        iron: '16%',
    },
];
</script>

    
<template>
    <div>
        <v-data-table :headers="headers" :items="desserts" item-value="id" show-expand>
            <template v-slot:expanded-row="{ columns, item }">
              <tr>
                <td :colspan="columns.length">
                  <div>
                    Expanded content for {{ item.raw.name }}
                  </div>
                </td>
              </tr>
          </template>
        </v-data-table>
    </div>
</template>
