<script>
    // TODO: Complete the code
    export default { 
        data() {
            return {
                
            }
        },
        // Hint: insert properties task (Object) and idx (Number)
        props: {
            taskObj: Object,
        }
    }
</script>

<template>
    <!-- TODO: add your template code here --> 
    <div class="card">
        <div class="card-header" style="background-color: white;">
            <h5>Deadline: {{taskObj.deadline}}</h5>
        </div>
        <div class="card-body">
            <p class="card-text">{{ taskObj.desc }}</p>
            <slot></slot>
        </div>
    </div>
</template>


