<template>
    <div>
        <b-modal id="deletePassengerModal" title="Delete Passenger" ok-title="Delete Passenger" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this passenger? <br><br>
            Name: {{passenger.name}} <br>
            Age: {{passenger.age}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        passenger: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/passengers/' + this.passenger.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>