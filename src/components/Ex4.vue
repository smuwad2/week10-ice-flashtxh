<script>
    import taskTracker from "./subcomponents/TaskTracker.vue"
    export default {
        data() {
            return {
                desc: '',
                deadline: '',
                taskList: []
            }
        },
        methods: {
            add() {
                this.taskList.push( { 'desc': this.desc, 'deadline': this.deadline } );
                console.log(this.taskList);
                this.desc = '';
                this.deadline = '';
            },
            // TODO: Add a new method, to delete a task completed
            deletePost(description) {
                this.taskList = this.taskList.filter(obj => obj.desc !== description);
            }
        },
        components: {
            taskTracker,
        }

    }

</script>

<template>
    <div class="mb-3">
        <label for="desc" class="form-label">Task</label>
        <input type="text" class="form-control" id="desc" v-model='desc' placeholder="task">
    </div>
    <div class="mb-3">
        <label for="deadline" class="form-label">Deadline</label>
        <input type="date" class="form-control" id="deadline" v-model='deadline' placeholder="deadline">
    </div>

    <button type="button" @click="add()" class="btn btn-primary">Add New Task</button>
    <hr>

    <!-- TODO: Modify following code -->
    <div class="row">
        <task-tracker v-for="task in taskList" 
        :taskObj="task"
        :key="task.desc" class="col-4"><button class="btn btn-primary" @click="deletePost(task.desc)">Done</button></task-tracker>
    </div>
    

</template>

<style scoped>
   
</style>