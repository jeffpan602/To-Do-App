<template>
    <v-app style='margin: 30px'>
        <v-card>
            <!--panel header-->
            <v-card-title class='headline primary' primary-title style="color: white;">
                <v-spacer />
                <span class="fa-solid fa-bars" /> &nbsp; FRAMEWORKS
                <v-spacer />

                <v-btn @click="addTaskDialog" color="primary" elevation="1">
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
                            <td class="text-center">{{ task.date }}</td>
                            <td class="text-center">{{ task.priority }}</td>
                            <td class="text-center">
                                <v-layout justify-center>
                                    <v-checkbox v-model="tasks[index].isComplete" />
                                </v-layout>
                            </td>
                            <td>
                                <v-layout justify-center v-if="!tasks[index].isComplete">
                                    <v-btn class="button mt-4" color="primary" elevation="1" small
                                        @click="editTaskDialog(index)">
                                        <span class="fa-solid fa-pen-to-square" /> UPDATE
                                    </v-btn>
                                </v-layout>
                                <v-layout justify-center>
                                    <v-btn class="delete button mb-2" color="error" elevation="1" small
                                        @click="deleteTask(index)">
                                        <span class="fa-solid fa-circle-xmark" /> DELETE
                                    </v-btn>
                                </v-layout>
                            </td>
                        </tr>
                    </tbody>
                </template>
            </v-simple-table>
        </v-card>
        <modalDialog v-show="isVisible" @close="closeModalDialog" @addTask="addTask" :isAddTask=isAddTask
            @editTask="editTask" :existing_description=description :existing_date=date :existing_priority=priority
            :tasks=tasks />





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
        addTaskDialog() {
            this.isAddTask = true
            this.showModalDialog()
        },
        showModalDialog() {
            this.isVisible = true
        },
        closeModalDialog() {
            this.isVisible = false
        },
        addTask(title, description, date, priority) {
            this.tasks.push({
                title: title,
                description: description,
                date: date,
                priority: priority,
                isComplete: false,
            })
            this.$toasted.success("The task has been sucessfully added!")
        },
        deleteTask(index) {
            this.tasks.splice(index, 1)
            this.$toasted.success("The task has been successfully deleted!")
        },
        editTaskDialog(index) {
            this.taskIndex = index
            this.isAddTask = false
            this.description = this.tasks[this.taskIndex].description
            this.date = this.tasks[this.taskIndex].date
            this.priority = this.tasks[this.taskIndex].priority
            this.showModalDialog();
        },
        editTask(description, date, priority) {
            this.tasks[this.taskIndex].description = description
            this.tasks[this.taskIndex].date = date
            this.tasks[this.taskIndex].priority = priority
            this.$toasted.success("The task has been successfully updated!")
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
                    description: 'desc',
                    date: '11/21/2022',
                    priority: 'high'
                }
            ],
            title: '',
            description: '',
            date: '',
            priority: 'low',
            taskIndex: ''
        };

    }
}
</script>

<style>
.delete {
    width: 90px;
}
</style>