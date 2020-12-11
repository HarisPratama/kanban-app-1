<template>
    <div class="home-page mt-5" id="home-page">
                <div v-if="errorMessage != ''" class="alert alert-danger alert-dismissible fade show" role="alert">
                    {{errorMessage}}
                    <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="row justify-content-center">
                    <div class="col-lg-3">
                        <div class="card d-flex flex-column">
                            <div class="card-header">
                                <h5>Backlog</h5>
                                <div class="add-task">
                                    <button class="btn" style="border-radius: 50%;" @click="show = !show" ><i class="fas fa-plus"></i></button>
                                </div>
                                <transition name="fade">  
                                    <div v-show="show" class="mt-3" id="form-add-task">
                                        <form @submit.prevent="addTask" action="" class="mt-3">
                                            <div class="form-group">
                                                <input v-model="taskAdd.title" placeholder="title" type="text" style="width: 100%;" class="form-control">
                                            </div>
                                            <button type="submit" style="border-radius: 50%;" class="btn"><i class="fas fa-save"></i></button>
                                            <button type="reset" @click="show = !show" style="border-radius: 50%;" class="btn"><i class="far fa-window-close"></i></button>
                                        </form>
                                    </div>
                                </transition>
                            </div>
                            <div class="card-body" id="card-tasks">
                                <div v-for="task in tasks" :key="task.id" v-show="task.category == 'backlog'" class="card border-0">
                                    <div class="card-body bg-white mt-3">
                                        <transition name="fade">  
                                            <div v-show="getTaskById.title != ''" v-if="task.id == getTaskById.id" id="form-edit-task">
                                                <form @submit.prevent="editTitleTask(task.id)" action="">
                                                    <div class="form-group">
                                                        <input v-model="getTaskById.title" placeholder="title" type="text" style="width: 100%;" class="form-control">
                                                    </div>
                                                    <button type="submit" class="btn"><i class="fas fa-save"></i></button>
                                                    <button type="reset" @click="getTaskById.title = !getTaskById.title" class="btn"><i
                                                            class="far fa-window-close"></i></button>
                                                </form>
                                            </div>
                                        </transition>
                                        <h5 class="card-title">{{task.title}}</h5>
                                      <p class="card-text"><img class="" alt="profile" width="20px"> {{task.User.firstName}} {{task.User.lastName}}</p>
                                    </div>
                                    <div class="card-footer border-0 bg-light">
                                        <button @click="getById(task.id)" class="btn text-success"><i class="fas fa-edit"></i></button>
                                        <button @click="deleteTask(task.id)" class="btn text-danger"><i class="fas fa-trash-alt"></i></button>
                                        <button @click="changeCategory('product', task.id)" class="btn text-info"><i class="fas fa-arrow-right"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-3">
                        <div class="card">
                            <div class="card-header">
                                <h5>Product</h5>
                            </div>
                            <div class="card-body bg-secondary">
                                <div v-for="task in tasks" :key="task.id" v-show="task.category == 'product'" class="card">
                                    <div class="card-body bg-white">
                                        <transition name="fade">
                                            <div v-show="getTaskById.title != ''" v-if="task.id == getTaskById.id" id="form-edit-task">
                                                <form @submit.prevent="editTitleTask(task.id)" action="">
                                                    <div class="form-group">
                                                        <input v-model="getTaskById.title" placeholder="title" type="text" style="width: 100%;"
                                                            class="form-control">
                                                    </div>
                                                    <button type="submit" class="btn"><i class="fas fa-save"></i></button>
                                                    <button type="reset" @click="getTaskById.title = !getTaskById.title" class="btn"><i
                                                            class="far fa-window-close"></i></button>
                                                </form>
                                            </div>
                                        </transition>
                                      <h5 class="card-title">{{task.title}}</h5>
                                    <p class="card-text"><img class="" alt="profile" width="20px"> {{task.User.firstName}}
                                        {{task.User.lastName}}</p>
                                    </div>
                                    <div class="card-footer border-0 bg-light">
                                        <button @click="getById(task.id)" class="btn text-success"><i class="fas fa-edit"></i></button>
                                        <button @click="deleteTask(task.id)" class="btn text-danger"><i class="fas fa-trash-alt"></i></button>
                                        <button @click="changeCategory('development', task.id)" class="btn text-info"><i
                                                class="fas fa-arrow-right"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-3">
                        <div class="card">
                            <div class="card-header">
                                <h5>Development</h5>
                            </div>
                            <div class="card-body bg-secondary">
                                <div v-for="task in tasks" :key="task.id" v-show="task.category == 'development'" class="card">
                                    <div class="card-body bg-white">
                                        <transition name="fade">
                                            <div v-show="getTaskById.title != ''" v-if="task.id == getTaskById.id" id="form-edit-task">
                                                <form @submit.prevent="editTitleTask(task.id)" action="">
                                                    <div class="form-group">
                                                        <input v-model="getTaskById.title" placeholder="title" type="text" style="width: 100%;"
                                                            class="form-control">
                                                    </div>
                                                    <button type="submit" class="btn"><i class="fas fa-save"></i></button>
                                                    <button type="reset" @click="getTaskById.title = !getTaskById.title" class="btn"><i
                                                            class="far fa-window-close"></i></button>
                                                </form>
                                            </div>
                                        </transition>
                                      <h5 class="card-title">{{task.title}}</h5>
                                    <p class="card-text"><img class="" alt="profile" width="20px"> {{task.User.firstName}}
                                        {{task.User.lastName}}</p>
                                    </div>
                                    <div class="card-footer border-0 bg-light">
                                        <button @click="getById(task.id)" class="btn text-success"><i class="fas fa-edit"></i></button>
                                        <button @click="deleteTask(task.id)" class="btn text-danger"><i class="fas fa-trash-alt"></i></button>
                                        <button @click="changeCategory('done', task.id)" class="btn text-info"><i class="fas fa-arrow-right"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-3">
                        <div class="card">
                            <div class="card-header">
                                <h5>Done</h5>
                            </div>
                            <div class="card-body bg-secondary">
                                <div v-for="task in tasks" :key="task.id" v-show="task.category == 'done'" class="card">
                                    <div class="card-body bg-white">
                                        <transition name="fade">
                                            <div v-show="getTaskById.title != ''" v-if="task.id == getTaskById.id" id="form-edit-task">
                                                <form @submit.prevent="editTitleTask(task.id)" action="">
                                                    <div class="form-group">
                                                        <input v-model="getTaskById.title" placeholder="title" type="text" style="width: 100%;"
                                                            class="form-control">
                                                    </div>
                                                    <button type="submit" class="btn"><i class="fas fa-save"></i></button>
                                                    <button type="reset" @click="getTaskById.title = !getTaskById.title" class="btn"><i
                                                            class="far fa-window-close"></i></button>
                                                </form>
                                            </div>
                                        </transition>
                                      <h5 class="card-title">{{task.title}}</h5>
                                    <p class="card-text"><img class="" alt="profile" width="20px"> {{task.User.firstName}}
                                        {{task.User.lastName}}</p>
                                    </div>
                                    <div class="card-footer border-0 bg-light">
                                        <button @click="getById(task.id)" class="btn text-success"><i class="fas fa-edit"></i></button>
                                        <button @click="deleteTask(task.id)" class="btn text-danger"><i class="fas fa-trash-alt"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
    </div>
</template>

<script>
export default {
    name: 'HomePage',
    data(){
        return {
            show: false,
            showEdit: false,
            server: 'http://localhost:3000',
            tasks: '',
            taskAdd: {
                title: ''
            },
            getTaskById: {
                id: '',
                title: ''
            },
            errorMessage: ''
            }
    },
    methods: {
        logout(){
            localStorage.clear();
            swal('Success logout');
            this.page = 'login-page';
        },
        fetchTasks() {
            axios({
                method: 'GET',
                url: this.server + '/task',
                headers: {
                    access_token: localStorage.getItem('access_token')
                }
            })
            .then(res => {
                this.tasks = res.data;
            })
            .catch(err => {
                swal('Something wrong');
            })
        },
        addTask(){
            axios({
                method: 'POST',
                url: this.server + '/task',
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                data: {
                    title: this.taskAdd.title
                }
            })
            .then(res => {
                if (res) {
                    swal('Success!! added task');
                    this.show = false;
                    this.fetchTasks();
                    console.log(res);
                } else {
                    swal('Oops!! something wrong');
                }
            })
            .catch(err => {
                this.show = false;
                this.fetchTasks();
                this.errorMessage = err.response.data.message;
            })
        },
        getById(id){
            axios({
                method: 'GET',
                url: this.server + `/task/${+id}`,
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                params: {
                    id: +id
                }
            })
            .then(resp => {
                this.showEdit = true;
                this.getTaskById.title = resp.data.title;
                this.getTaskById.id = resp.data.id;
            })
            .catch(err => {
                swal(err.response.data.message);
            })
        },
        changeCategory(category, id){
            axios({
                method: 'PATCH',
                url: this.server + `/task/${+id}`,
                params: +id,
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                data: {
                    category: category
                }
            })
            .then(resp => {
                console.log(category);
                swal(`Task move to ${category}`);
                this.fetchTasks();
            })
            .catch(err => {
                swal(err.response.data.message);
            })
        },
        editTitleTask(id){
            axios({
                method: 'PUT',
                url: this.server + `/task/${+id}`,
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                params: {
                    id: +id
                },
                data: {
                    title: this.getTaskById.title
                }
            })
            .then(resp => {
                this.getTaskById.title = '';
                this.fetchTasks();
            })
            .catch(err => {
                swal(err.response.data.message);
            })
        },
        deleteTask(id){
            swal({
                title: "Are you sure?",
                text: "Once deleted, you will not be able to recover this imaginary file!",
                icon: "warning",
                buttons: true,
                dangerMode: true,
            })
            .then((willDelete) => {
                if (willDelete) {
                    return axios({
                        method: 'DELETE',
                        url: this.server + `/task/${+id}`,
                        params: {
                            id: +id
                        },
                        headers: {
                            access_token: localStorage.getItem('access_token')
                        }
                    })
                }
            })
            .then(resp => {
                if (resp) {
                    swal("Success! task has been deleted!", {
                        icon: "success",
                    });
                } else {
                    swal("Your task is safe!");
                }

                this.fetchTasks();
            })
            .catch(err => {
                swal(err.response.data.message);
            });
        }
    }
}
</script>

<style>

</style>