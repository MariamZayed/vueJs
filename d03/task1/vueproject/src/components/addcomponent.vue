<template>
    <div>
        <button class="btn btn-success w-100" data-bs-toggle="modal" data-bs-target="#addnewstudentmodal">Add Student</button>
        <div class="modal fade" id="addnewstudentmodal" data-bs-backdrop="static" data-bs-keyboard="false">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header bg-info">
                        <h6 class="text-center w-100">Adding New Student</h6>
                    </div>
                    <div class="modal-body">
                        <input type="text" class="form-control my-1" v-model="stdname" placeholder="Name"/>
                        <input type="text" class="form-control my-1" v-model="stdcity" placeholder="City"/>
                    </div>
                    <div class="modal-footer text-end">
                        <button class="btn btn-success" data-bs-dismiss="modal" @click="sendDataToParent()">Add</button>
                        <button class="btn btn-danger" data-bs-dismiss="modal">Cancel</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    data:()=>({
        stdname:'',
        stdcity:''
    }),
    methods:{
        sendDataToParent(){
            let createdstudent = {name:this.stdname,city:this.stdcity};
            this.$emit("addstudentraised",createdstudent);
            this.stdname=''; this.stdcity='';
        }
    }
}
</script>