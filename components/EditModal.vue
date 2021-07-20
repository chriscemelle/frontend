<template>
    <div>

        <b-modal id="editModal" title="Game Entry" ok-title="Save" @ok="onSubmit">
            <form action="#">
                <b-form-group
                    label="Game Name"
                    label-for="game_name"
                    >
                    <b-form-input id="game_name" v-model="game.game_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                    >
                    <b-form-input id="description" v-model="game.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Player Name"
                    label-for="player_name"
                    >
                    <b-form-input id="player_name" v-model="game.player_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Player ID"
                    label-for="player_id"
                    >
                    <b-form-input id="player_id" v-model="game.player_id" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Played On"
                    label-for="played_on"
                    >
                    <b-form-input id="played_on" type="number" v-model="game.played_on" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Status"
                    label-for="status"
                    >
                    <b-form-select id="status" v-model="game.status" :options="statuses"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        game: {}

    },
    
    data() {
        return {
            game: {},
            statuses: [
                { value: 'online', text: 'Online' },
                { value: 'offline', text: 'Offline' },
                
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('http://localhost:8000/api/games/' + this.game.id, this.game)
            .then((res)=>{
                if(res.status==202) {
                    alert('Update Successfully')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
    
}
</script>