<template>
    <div class='form-container'>   
        <v-form @submit.prevent='submit'>
            <v-text-field
            v-model='name'
            label="Bot Name"
            required
            ></v-text-field>
            <v-text-field
            v-model='attack'
            label="Attack Value"
            required
            type='number'
            ></v-text-field>
            <v-text-field
            v-model='health'
            label="Health Value"
            required
            ></v-text-field>
            <v-btn
            :disabled="!valid"
            type='number'
            >
            submit
            </v-btn>
            <v-btn @click="clear">clear</v-btn>
        </v-form>
    </div>
</template>

<script>
export default {
    props: ['addBot'],
    data() {
        return {
            name: '',
            attack: null,
            health: null
        }
    },
    methods: {
        clear() {
            this.name = '';
            this.attack = null;
            this.health = null;
        },
        submit() {
            this.addBot({name: this.name, attack: this.attack, health: this.defense});
            this.$emit('switchTab')
        }
    },
    computed: {
        valid() {
            return this.name && this.attack && this.health ? true : false;
        }
    }
}
</script>

<style scoped>
.form-container {
    width: 100%;
    display: flex;
    justify-content: center;
}
form {
    margin-top: 50px;
    width: 400px;
    background-color: white;
    padding: 10px 20px;
    border-radius: 2px;
    box-shadow: 0px 3px 1px -2px rgba(0,0,0,0.2), 0px 2px 2px 0px rgba(0,0,0,0.14), 0px 1px 5px 0px rgba(0,0,0,0.12);
}
</style>