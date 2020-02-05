<template>
     <div class="container">
        <div class="row align-content-center">
            <div class="col-sm-5">
                <div class="card shadow p-4">
                    <div class="row">
                        <div class="col-md-12">
                            <div class="well">
                                <h2>My ToDo</h2>
                                <form>
                                    <div class="form-group">
                                        <label for="todoitem">Plan Your Day!!</label>
                                        <input type="text" v-model="myList.input" class="form-control" placeholder="E.g Have a meeting" />
                                    </div>
                                    <button type="button" v-if="display" v-on:click="update" class="btn btn-secondary">Update</button>
                                    <button v-else type="button" v-on:click="addDoing()" class="btn btn-primary">ADD ToDo</button>
                                </form>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-12 mt-5">
                            <h2>Doing</h2>
                            <ul class="list-group">
                                <li v-for="(Do, index) in Doing" :key="index" class="list-group-item">
                                    <p>{{ index + 1 }}- <span @click="strikeThrough(index)" class="myHov" >{{ Do }}</span>
                                    <span @click="deleteDoing(index)"><button type="button" class="close"  aria-label="Close"> <span aria-hidden="true">&times;</span></button></span>
                                    <span @click="strikeThrough(index)" button type="button" class="btn btn-success"/>
                                    <span class="mys mr-2" @click="editDoing(Do)">Edit</span></p>  

                                </li>
                            </ul>
                        </div>
                    </div>

                      <div class="row">
                        <div class="col-md-12 mt-5">
                            <h2>Done</h2>
                            <ul class="list-group">
                                <li v-for="(todo, i) in Done" :key="i" class="list-group-item">
                                    <p>{{ i + 1 }}-  <span  class="myHov" >{{ todo }}</span>
                                    <!-- <span @click="deleteTodos(index)"><button type="button" class="close" aria-label="Close"><span aria-hidden="true">&times;</span></button></span>
                                    <span class="mys mr-2" @click="editTodos(todo)">Edit</span> --></p> 
                                </li>
                            </ul>
                        </div>
                    </div>


                </div>
            </div>
        </div>
   </div>
</template>

<script>
export default {
        data () {
            return {
                myList:{
                    input: "",
                },
                Doing: [],
                Done: [],
                display: false,
                completed: true,
                todos: [],
                indexOfTheItemWeWantToEdit: null,
                editText: null,
                complete: ''
            }
        },
        methods: {
            addDoing() {
                if(this.myList.input === ''){
                    Swal.fire({
                        icon: 'error',
                        title: 'Oops...',
                        text: 'Please insert your plans',
                        // footer: '<a href>Why do I have this issue?</a>'
                    })
                }else{
                    this.Doing.push(this.myList.input);
                    this.myList.input = "";
                }
            },
            deleteDoing(index){
                var item = this.Doing[index];
                this.Doing.splice(index, 1);
                // this.Done.push(this.item);
            },
            editDoing(id){
                this.myList.input = id;
                this.display = true;
                this.indexOfTheItemWeWantToEdit = this.Doing.indexOf(id);
                console.log('this is the index ' + this.indexOfTheItemWeWantToEdit);
            },
            update(){
                Swal.fire(
                    'Good job!',
                    'You Updated your plan',
                    'success'
                )
                this.display = false;
                this.Doing[this.indexOfTheItemWeWantToEdit] = this.myList.input;
                this.myList.input = "";
            },
            strikeThrough(index){
                var item = this.Doing[index];
                this.Done.push(item);
                this.Doing.splice(index, 1);
            },

        }
}
</script>
<style scoped>
.mys{
    float: right;
    width: 70px;
    height: 40px;
    padding: 2px;
    text-align: center;
    color: gray;
    border-radius: 10px;
}
.myHov2{
    text-decoration: line-through;
}
.myHov:hover, .myHov2:hover{
    cursor: pointer;
}
.mys:hover{
    cursor: pointer;
}
@media (max-width: 575.98px) {
    span{
        font-size: 15px !important;
    }
    .mys{
        font-size: 15px !important;
        padding: 5px !important;
    }
}
</style>


