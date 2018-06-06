<template>
    <v-card class='card'>
        <v-card-title primary-title>
        <div>
            <h3>{{bot.name}}</h3>
            <br>
            <span>Attack: {{bot.attack}}</span>
            <br>
            <span>Health: {{bot.health}}</span>
        </div>
        </v-card-title>
        <v-card-actions>
        <v-btn flat @click='select'>Select</v-btn>
        <v-btn flat color="purple" @click='retire'>Retire</v-btn>
        <v-spacer></v-spacer>
        </v-card-actions>
    </v-card>
</template>

<script>
    export default {
        props: ['bot'],
        methods: {
            retire() {
                this.$emit('retire')
            },
            select() {
                this.$emit('selectBot', this.bot)
            }
        }
    }
</script>

<style scoped>
.card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>