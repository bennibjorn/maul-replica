<template>
    <v-card
        :color="color"
        class="d-flex flex-column"
        :style="{ width: width, margin: '8px'}"
        @click="$emit('click')"
    >
        <v-card-title>{{ dish.ShortDescriptionByLang[lang] }}</v-card-title>
        <v-card-subtitle><b>{{ dish.RestaurantName }}</b></v-card-subtitle>
        
        <v-card-text class="flex-grow-1">
            <v-row>
                <v-col>{{ dish.DescriptionByLang[lang] }}</v-col>
            </v-row>
            <v-row v-if="dish.Allergens.length > 0">
                <v-col>
                    <v-chip
                        v-for="allergen in dish.Allergens"
                        :key="allergen"
                        color="grey lighten-4"
                        class="mr-2 mb-2"
                        small
                        outlined
                    >
                        <v-icon left small color="grey">mdi-alert-circle</v-icon>
                        <span class="grey--text">{{ allergen }}</span>
                    </v-chip>
                </v-col>
            </v-row>
        </v-card-text>

        <v-card-actions class="pt-0">
            <v-row v-if="dish.DietTypes.length > 0" justify="center">
                <v-chip
                    v-for="diet in dish.DietTypes"
                    :key="diet"
                    :color="dietTypeColors[diet] || '#F0F0F0'"
                    class="mr-2"
                    small
                >
                    {{ diet.charAt(0).toUpperCase() + diet.slice(1) }}
                </v-chip>
            </v-row>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    name: 'MenuCard',
    props: {
        dish: {
            type: Object,
            required: true
        },
        lang: {
            type: String,
            default: 'is'
        },
        color: {
            type: String,
            default: undefined
        },
        width: {
            type: String,
            default: '30%'
        }
    },
    data() {
        return {
            dietTypeColors: {
                'omnivore': '#FFE4E1',
                'vegan': '#E0F4E0',
                'pescatarian': '#E6F3FF',
                'low-carb': '#FFF0DB'
            }
        }
    }
}
</script>

<style scoped>
.v-card {
    display: flex;
    flex-direction: column;
}

.v-card__text {
    flex-grow: 1;
}

.v-card__actions {
    margin-top: auto;
    padding-bottom: 16px;
}
</style>
