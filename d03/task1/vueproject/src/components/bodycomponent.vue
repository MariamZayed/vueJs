<template>
    <div>
        <addcomponent @addstudentraised="addNewStudent"/>
        <table class="table" v-if="isFormVisible==false">
            <thead>
                <tr>
                    <th>#</th>
                    <th>name</th>
                    <th>city</th>
                    <th>ِAction</th>
                </tr>
            </thead>
            <tbody >
                    <tr v-for="student in students" :key="student.id">
                        <td>{{ student.id }}</td>
                        <td>{{ student.name }}</td>
                        <td>{{ student.city }}</td>
                        <td><i class="fa-solid fa-pen-to-square  actions" data-bs-toggle="modal" data-bs-target="#updatemodal" @click="filldata(student)"></i> |
                            <i class="fa-solid fa-trash actions" @click="deleteStudent(student.id)"></i></td>
                    </tr>                
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="4">
                        <h5 class="alert alert-info col-12 text-center"> {{msg}} {{ students.length }}</h5>
                    </td>
                </tr>
            </tfoot>
        </table>
        <!-- edit modal -->
        <div class="modal fade" id="updatemodal" data-bs-backdrop="static" data-bs-keyboard="false">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header bg-warning">
                        <h6 class="text-center w-100">updating...</h6>
                    </div>
                    <div class="modal-body">
                        <input type="text" disabled class="form-control my-1" v-model="stdid" placeholder="Name"/>
                        <input type="text" class="form-control my-1" v-model="stdname" placeholder="Name"/>
                        <input type="text" class="form-control my-1" v-model="stdcity" placeholder="City"/>
                    </div>
                    <div class="modal-footer text-end">
                        <button class="btn btn-success" data-bs-dismiss="modal" @click="updateStudentDate()">Update</button>
                        <button class="btn btn-danger" data-bs-dismiss="modal">Cancel</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import addcomponent from './addcomponent.vue';
export default {
    data(){
        return{
            msg:'total num of students = ',
            students:[],
            isFormVisible:false,
            stdid:"",
            stdname:"",
            stdcity:"",

        }
    },
    async created(){
        let resp = await fetch("http://localhost:4000/students");
        let respobject = await resp.json();
        this.students=respobject; 
    },
    methods:{
        filldata(student){
            this.stdid=student.id;
            this.stdname=student.name;
            this.stdcity=student.city;
        },
        async deleteStudent(_id){
            if(confirm("are you sure you want to delete?")){
                await fetch(`http://localhost:4000/students/${_id}`,{
                method:"DELETE",
                });
                //update UI
                this.students.splice(this.students.findIndex(std=>std.id==_id),1);//only delete one element
            }
            
        },
        async updateStudentDate(){
            let updatedstudent = {id:this.stdid,name:this.stdname,city:this.stdcity};
            //put
            await fetch(`http://localhost:4000/students/${this.stdid}`,{
                method:"PUT",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(updatedstudent)// send this obj in body
            });
            //update UI, db is updated, ui is not 
            this.students.find(student=>student.id==this.stdid).name=this.stdname;
            this.students.find(student=>student.id==this.stdid).city=this.stdcity;
        },
        async addNewStudent(e){
            let createdObject = {id:this.students[this.students.length-1].id+100,name:e.name,city:e.city};
            //post
            await fetch("http://localhost:4000/students",{
                method:"POST",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(createdObject)// send this obj in body
            });
            //update UI, db is updated, ui is not 
            this.students.push(createdObject);
            
        },
    },
    components:{
        addcomponent
    }
}
</script>

<style scoped>
.actions:hover{
    color: red;
    cursor:pointer;
}
</style>