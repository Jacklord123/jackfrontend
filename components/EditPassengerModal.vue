<template>
    <div>
        <b-modal id="editPassengerModal" title="Edit Passenger" ok-title="Save Passenger" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="passenger.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Age" label-for="age">
                <b-form-input id="age" v-model="passenger.age" trim></b-form-input>
                </b-form-group>


                <b-form-group label="Address" label-for="address">
                <b-form-input id="address" v-model="passenger.address" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Contact" label-for="contact">
                <b-form-select v-model="passenger.contact" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        passenger: {}
    },
    data() {
        return {
            options: [
                {value: 'programmer', text: 'programmer'},
                {value: 'designer', text: 'designer'},
               
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/passengers/' + this.passenger.id, this.passenger)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>