<template>
    <table class="table">
        <thead>
            <tr>
                <th>#</th>
                <th>name</th>
                <th>city</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="student in students" :key="student.id">
                <td>{{ student.id }}</td>
                <td>{{ student.name }}</td>
                <td>{{ student.city }}</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="3">
                    <h5 class="alert alert-info col-12 text-center"> {{msg}} {{ students.length }}</h5>
                </td>
            </tr>
        </tfoot>
    </table>
</template>

<script>
import students from './../student';
export default {
    data(){
        return{
            msg:'total num of students = ',
            students
        }
    }
}
</script>