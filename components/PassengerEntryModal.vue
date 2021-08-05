<template>
    <div>
        <b-button v-b-modal.PassengerEntryModal variant="primary">Add Passenger</b-button>

        <b-modal id="PassengerEntryModal" title="Passenger Entry" ok-title="Save Passenger" @ok="onSubmit">
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
                <b-form-select v-model="pasenger.contact" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            passenger: {},
            options: [
                {value: 'email', text: 'email'},
                {value: 'mobile number', text: 'mobile number'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('/api/passengers', this.passenger)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added an passenger')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>