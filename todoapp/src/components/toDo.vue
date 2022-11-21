<template>
    <v-app style='margin: 30px'>
        <v-card>
            <!--panel header-->
            <v-card-title class='headline primary' primary-title style="color: white;">
                <v-spacer />
                <span class="fa-solid fa-bars" /> &nbsp; FRAMEWORKS
                <v-spacer />

                <v-btn @click="showModalDialog" color="primary" elevation="1">
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
                        <tr v-for="(task, index) in tasks" :key="index">
                            <td class="text-center">{{ task.title }}</td>
                            <td class="text-center">{{ task.description }}</td>
                            <td class="text-center">{{ task.deadline }}</td>
                            <td class="text-center">{{ task.priority }}</td>
                            <td class="text-center">
                                <v-layout justify-center>
                                    <v-checkbox v-model="tasks[index].isComplete" />
                                </v-layout>
                            </td>
                        </tr>
                    </tbody>
                </template>
            </v-simple-table>
        </v-card>
        <modalDialog v-show="isVisible" @close="closeModalDialog" :isAddTask=isAddTask />
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
    methods: {
        showModalDialog() {
            this.isVisible = true
            this.isAddTask = true
        },
        closeModalDialog() {
            this.isVisible = false
        },
        addTask(title, description, deadline, priority) {
            this.tasks.push({
                title: title,
                description: description,
                deadline: deadline,
                priority: priority,
                isComplete: false,
            });
        }
    },
    //watchers
    watch: {},
    //computed
    computed: {},
    //global vars
    data() {
        return {
            isVisible: false,
            isAddTask: true,

            tasks: [
                {
                    title: 'task1',
                    description: 'description1',
                    deadline: '11/20/22',
                    priority: 'low'
                }
            ],
            title: '',
            description: '',
            deadline: '',
            priority: 'low',
            taskIndex: ''
        };

    }
}
</script>