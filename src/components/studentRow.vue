<template>
    <tr v-bind:class="{present: student.present, absent: !student.present}">   <!-- Add style with css when 'student.present' is selected-->
                <td>{{ student.name }}</td>
                <td>{{ student.starID }}</td> 
                <td> <input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedOrLeft(student, $event.target.checked)"></td>
                <td v-show="edit"> <img v-on:click="deleteStudent" src="@/assets/delete.png"> </td>
    </tr>
</template>

<script>
export default {        
    name: 'StudentRow',
    props: {
        student: Object,
        edit: Boolean
    },
    methods: {
        arrivedOfLeft(student, present) {
            this.$emit('student-arrived-or-left', student, present)
        },
        deleteStudent() {
            if (confirm(`Delete ${this.student.name}?`)) {
                this.$emit('delete-student', this.student)
            }
            this.$emit('delete-students', this.student)
        }
    }
}
</script>

<style scoped>
.present {
    color: grey;
    font-style: italic;
}
.absent{
    color: black;
    font-weight: bold;
}

img {
    height: 35px;
}
</style>
