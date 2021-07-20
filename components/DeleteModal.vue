<template>
    <div>

        <b-modal id="deleteModal" title="Delete Game" ok-title="Save" @ok="onDelete" ok-variant="danger">
            Are You Sure Want to delete this?
            <br>
            <br>
            <h1>{{game.game_name}}</h1>
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        game: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('http://localhost:8000/api/games/' + this.game.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Game is deleted Successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
    
}
</script>