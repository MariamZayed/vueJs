<template>
    <table class="table" v-if="isFormVisible==false">
        <thead>
            <tr>
                <th>#</th>
                <th>name</th>
                <th>city</th>
            </tr>
        </thead>
        <tbody >
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
            <tr>
                <td colspan="3">
                    <button  @click.prevent="isFormVisible=true" class=" btn btn-primary">
                    Add to table
                    </button>
                </td>
            </tr>
        </tfoot>
    </table>
    <div v-if="isFormVisible==true">
        <button @click.prevent="isFormVisible=false" class="btn btn-primary" > Show Student Table</button>    
        <form method="get" action="#" >
            <div class="mb-3">
                <label class="form-label">id</label>
                <input type="text" class="form-control" v-model="student.id" id="id">
            </div>
            <div class="mb-3">
                <label class="form-label">Name</label>
                <input type="text" class="form-control" v-model="student.name" id="name">
            </div>
            <div class="mb-3">
                <label class="form-label">city</label>
                <input type="text" class="form-control" v-model="student.city" id="city">
            </div>
            <button type="submit" class="btn btn-primary" @click.prevent=addToStudentTable(student)>Submit</button>
        </form>
    </div>
</template>

<script>
import students from './../student';
export default {
    data(){
        return{
            msg:'total num of students = ',
            students,
            isFormVisible:false,
            student:{
                id:'',
                name:"",
                city:''
            }
        }
    },
    methods:{
        addToStudentTable(student){
            this.students.push(student);
            console.log(this.students.length);
        },
    },
}
</script>