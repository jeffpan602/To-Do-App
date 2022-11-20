<template>
    <v-app style='margin:30px'>
        <v-card>
            <!--panel header-->
            <v-card-title class='headline primary' primary-title style="color: white;">
                <v-spacer />
                <span class="fa-solid fa-bars" /> &nbsp; FRAMEWORKS
                <v-spacer />

                <v-btn color="primary" elevation="1">
                    <span class="fa-solid fa-circle-plus" />ADD
                </v-btn>

            </v-card-title>
            <!--panel body-->
            <v-simple-table style='margin: 20px;'>
                <template v-slot:default>
                    <!--table header-->
                    <thead>
                        <tr>
                            <th class="column text-center"> Title </th>
                            <th class="column text-center"> Description </th>
                            <th class="column text-center"> Deadline </th>
                            <th class="column text-center"> Priority </th>
                            <th class="column text-center"> Is Complete </th>
                            <th class="column text-center"> Action </th>
                        </tr>
                    </thead>
                    <!--table body-->
                    <tbody>
                        <tr>
                            <td>{{ }}</td>
                        </tr>
                    </tbody>
                </template>
            </v-simple-table>
        </v-card>
        <modalDialog />
    </v-app>
</template>
<script>
import modalDialog from './modalDialog.vue';
//master
export default {
    name: 'toDo',
    components: {
        modalDialog
    },
    //life cycles
    created() { },
    //methods
    methods: {},
    //watchers
    watch: {},
    //computed
    computed: {},
    //global vars
    data() {
        return {

        };

    },
}
</script>