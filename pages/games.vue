<template>
    <div>
        <NavBar />

        <div class="container">
            <EditModal :game="selectedGame" />
            <DeleteModal :game="selectedGame" @onDeleted="getAll" />
            
            <h1>
                <GameEntryModal class="float-right" @onAdd="getAll" />
                Game
            </h1>

            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Game Name</th>
                        <th>Description</th>
                        <th>Player Name</th>
                        <th>Player Id</th>
                        <th>Played On</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="game in games" :key="game.id">
                        <td>{{game.game_name}}</td>
                        <td>{{game.description}}</td>
                        <td>{{game.player_name}}</td>
                        <td>{{game.player_id}}</td>
                        <td>{{game.played_on}}</td
                        <td>{{game.status}}</td>
                        <td>
                            <b-button @click="onEdit(game)" variant="info" size="sm">Edit</b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(game)" variant="danger" size="sm">Delete</b-button>
                        </td>
                    </tr>
                </tbody>

            </table>

        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            games: [],
            selectedGame: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('http://localhost:8000/api/games')
            .then((res)=>{
                if(res.status==200) {
                    this.games = res.data
                    console.log(this.games)
                }
            })
        },
        onEdit(selectedGame) {
            this.selectedGame = selectedGame;
            this.$bvModal.show('editModal')
        },
        onDelete(selectedGame) {
            this.selectedGame = selectedGame;
            this.$bvModal.show('deleteModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>