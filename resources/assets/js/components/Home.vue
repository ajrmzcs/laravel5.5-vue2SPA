<template>
    <div class="container">
        <div class="columns">
            <div class="column">
                <div class="message" v-for="status in statuses">
                    <div class="message-header">

                        <p>
                            {{ status.user.name }} said...
                        </p>
                        <p>
                            {{ status.created_at | ago | capitalize }}
                        </p>

                    </div>

                    <div class="message-body" v-text="status.body"></div>
                </div>

                <add-new-status @completed="addStatus"></add-new-status>

            </div>
        </div>
    </div>
</template>

<script>

    import moment from 'moment';
    import AddNewStatus from '../components/AddNewStatus.vue';

    export default {

        components: { AddNewStatus },

        data() {

            return  {

                statuses:[]

            }

        },

        filters: {

            ago(date) {

                return moment(date).fromNow();

            },

            capitalize(value) {

                return value.toUpperCase();

            }

        },

        created() {

            axios.get('/statuses')
                .then(response => this.statuses = response.data);


        },

        methods: {

            addStatus(status) {

                this.statuses.unshift(status);

                alert('Your status has been updated in the Home Page!!');

//                window.scrollTo(0, 0);

            }

        }
    }
</script>
