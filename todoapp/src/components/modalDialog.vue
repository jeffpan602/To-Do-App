<template>
    <div class="modalDialog-background">
        <div class="modalDialog">
            <v-card>
                <!-- panel header -->
                <v-card-title class='headline primary justify-left' primary-title style='color: white;'>
                    <div>
                        <span class="fa-solid fa-circle-plus" />Add Task
                    </div>
                </v-card-title>
                <!-- panel body-->
                <v-form ref="form" lazy-validation>
                    <v-layout class="elements mx-5 mb-0 mt-7">
                        <v-text-field label="Title" outlined v-model="title" required />
                    </v-layout>

                    <v-layout class="element mx-5 my-2">
                        <v-text-field label="Description" outlined v-model="description" required />
                    </v-layout>

                    <v-layout class="elements mx-5 my-0">
                        <v-menu ref="menu" :close-on-content-click="false" :return-value.sync="deadline"
                            transition="scale-transition" offset-y min-width="auto">
                            <template v-slot:activator="{ on, attrs }">
                                <v-text-field v-model="deadline" label="Deadline" append-icon="mdi-calendar"
                                    v-bind="attrs" v-on="on" readonly outlined required />
                            </template>
                            <v-date-picker v-model="date" no-title scrollable>
                                <v-spacer></v-spacer>
                                <v-btn text color="primary" @click="menu = false"> Cancel </v-btn>
                                <v-btn text color="primary" @click="$refs.menu.save(date)">OK</v-btn>
                            </v-date-picker>
                        </v-menu>
                    </v-layout>

                    <v-radio-group label="Priority" class="elements mx-4 my-0" v-model="priority">
                        <v-layout align-start row d-flex justify-space-between>
                            <v-radio label="Low" value="low" /> &nbsp;
                            <v-radio label="Med" value="med" /> &nbsp;
                            <v-radio label="High" value="high" />
                        </v-layout>
                    </v-radio-group>

                    <v-layout justify-end class="elements mx-2 mt-0 mb-2">
                        <div>
                            <v-btn color="primary" elevation="2" @click="addTask" class="mr-2">
                                <i class="fa-solid fa-circle-plus"></i> ADD
                            </v-btn>
                        </div>
                        <v-btn color="error" elevation="2" @click="closeModalDialog"> <span class="fa-solid fa-ban" />
                            CANCEL
                        </v-btn>
                    </v-layout>
                </v-form>
            </v-card>
        </div>
    </div>
</template>

<script>
export default {
    name: 'modalDialog',
    props: {
        isVisible: Boolean,
        isAddTask: Boolean
    }
}
</script>

<style>
.modalDialog-background {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modalDialog {
    background: white;
    box-shadow: 2px 2px 20px 2px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
}

.modalDialog {
    background: white;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
}

.element {
    margin: 15px 15px;
    padding: 0px;
}
</style>