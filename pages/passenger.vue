<template>
    <div>
        <NavBar />
        <EditPassengerModal :passenger="selectedPassenger" />
        <DeletePassengerModal :passenger="selectedPassenger" @onDeleted="getAll" />

        <div class="container">
            <h1>
                List of Passenger
            </h1>
            
            <PassengerEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Age</th>
                        <th>Address</th>
                        <th>Contact</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="passenger in passengers" :key="passenger.id">
                        <td>{{passenger.name}}</td>
                        <td>{{passenger.age}}</td>
                        <td>{{passenger.address}}</td>
                        <td>{{passenger.contact}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(passenger)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(passenger)" variant="danger" size="sm">
                                Delete
                            </b-button>
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
           passenger: [],
            selectedPassenger: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/passengers')
            .then((res)=>{
                if (res.status==200) {
                    this.passengers = res.data
                };
            })
        },
        onEdit(selectedPassenger) {
            this.selectedPassenger = selectedPassenger
            this.$bvModal.show('editPassengerModal')
        },
        onDelete(selectedPassenger) {
            this.selectedPassenger = selectedPassenger
            this.$bvModal.show('deletePassengerModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>