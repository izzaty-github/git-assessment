<template>
    <div>  
          
<div class="container">
    <div class="row justify-content-end">
    <div class="col-4">
            <button class=" btn-outline-primary" @click.prevent="previousChange()">Previous</button> 
    </div>
    <div class="col-4">
            <h3>{{page}} Of {{pages}} </h3>
    </div>
    <div class="col-4">
            <button class="btn-outline-primary" @click.prevent="nextChange()">Next</button>
    </div>
    </div>
</div>
        
        <button class="btn btn-primary m-2 fload-end" data-bs-toggle="modal" data-bs-target="#exampleModal"
        @click="addClick()"> Add User</button>

        <table class="table table-striped">
            <thead>
                <tr>
                    <th>
                        <div class="d-flex flex-row">
                            <input class="form-control m-2"
                            v-model="PostIdFilter"
                            v-on:keyup="FilterFn()"
                            placeholder="Filter Id">
                        </div>
                        Id</th>
                    <th>
                        <div class="d-flex flex-row">
                            <input class="form-control m-2"
                            v-model="PostNameFilter"
                            v-on:keyup="FilterFn()"
                            placeholder="Filter Name">
                        </div>
                        Name</th>
                    <th>Email</th>
                    <th>Gender</th>
                    <th>Status</th>
                    <th>Options</th>
                </tr>
            </thead>
                <tbody>
                    <tr v-for="user in users" :key="user.id">
                        <td>{{user.id}}</td>
                        <td>{{user.name}}</td>
                        <td>{{user.email}}</td>
                        <td>{{user.gender}}</td>
                        <td>{{user.status}}</td>
                        <td>
                             <div class="d-flex flex-row">

                            <button class="btn btn-light mr-1" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="editClick(user)"> 
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-square" viewBox="0 0 16 16">
                                <path d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"/>
                                <path fill-rule="evenodd" d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"/>
                                </svg> 
                            </button>

                            <button class="btn btn-primary m-2 fload-end" data-bs-toggle="modal" data-bs-target="exampleModal" @click="deleteClick(user.id)">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                                <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                                <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                                </svg>
                            </button>
                             </div>
                        </td>
                    </tr>
                </tbody>
            
        </table>

        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">

        <div class="modal-dialog modal-lg modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{modalTitle}}</h5>
                    <button class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>

                <div class="modal-body">
                    <div class="input-group mb-3">
                        <span class="input-group-text"> Name </span>
                        <input type="text" class="form-control" v-model="name">
                    </div>
                    <div class="input-group mb-3">
                        <span class="input-group-text"> Email </span>
                        <input type="text" class="form-control" v-model="email">
                    </div>
                    <div class="input-group mb-3">
                        <span class="input-group-text"> Gender </span>
                        <select class="form-select" v-model="gender">
                            <option selected>Open this select menu</option>
                            <option value="female">Female</option>
                            <option value="male">Male</option>
                        </select>
                    </div>
                    
                    <div class="input-group mb-3">
                        <span class="input-group-text"> Status </span>
                        <select class="form-select" v-model="status">
                            <option selected>Open this select menu</option>
                            <option value="active">Active</option>
                            <option value="inactive">Inactive</option>
                        </select>
                    </div>

                    <button @click="createClick()" v-if="id==0" class="btn btn-primary">Create</button>
                    <button @click="updateClick()" v-if="id!=0" class="btn btn-primary">Update</button>
                </div>
            </div>
        </div>

        </div>
        
    </div>
</template>

<script>
import Axios from 'axios'


export default {
  name: 'UserList',
  data(){
      return{
          users: [],
          modalTitle: "",
          name: "",
          email: "",
          gender: "",
          status: "",
          id:0,
          PostNameFilter: "",
          PostIdFilter: "",
          postsWithoutFilter: [],
          page: [],
          total: Number,
          pages: [],
          current: "",
          next: "",
          previous: "",
          user_id:"",

      }
  },
  methods: {
      async refreshPosts(){
          const headers = { 
        "Authorization": "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6",
        "Content-Type": "application/json",
        };
          Axios.get('https://gorest.co.in/public/v1/users/',{headers})
          .then((response) => {
               console.log(response.data.data)
                console.log(response.data.meta.pagination)

              this.users = response.data.data;
              this.page = response.data.meta.pagination.page;
              this.total = response.data.meta.pagination.total;
              this.pages = response.data.meta.pagination.pages;
              this.current = response.data.meta.pagination.links.current;
              this.next = response.data.meta.pagination.links.next;
              this.previous = response.data.meta.pagination.links.previous;

              this.postsWithoutFilter = response.data.data;
          })
          .catch((error) => {
              console.log(error)
          })
      },

      async nextChange(){
          const headers = { 
        "Authorization": "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6",
        "Content-Type": "application/json",
        };
          Axios.get(this.next,{headers})
          .then((response) => {
               console.log(response.data.data)
                console.log(response.data.meta.pagination)

              this.users = response.data.data;
              this.page = response.data.meta.pagination.page;
              this.total = response.data.meta.pagination.total;
              this.pages = response.data.meta.pagination.pages;
              this.current = response.data.meta.pagination.links.current;
              this.next = response.data.meta.pagination.links.next;
              this.previous = response.data.meta.pagination.links.previous;

              this.postsWithoutFilter = response.data.data;
          })
          .catch((error) => {
              console.log(error)
          })
      },

      async previousChange() {
           const headers = { 
        "Authorization": "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6",
        "Content-Type": "application/json",
        };
          Axios.get(this.previous,{headers})
          .then((response) => {
               console.log(response.data.data)
                console.log(response.data.meta.pagination)

              this.users = response.data.data;
              this.page = response.data.meta.pagination.page;
              this.total = response.data.meta.pagination.total;
              this.pages = response.data.meta.pagination.pages;
              this.current = response.data.meta.pagination.links.current;
              this.next = response.data.meta.pagination.links.next;
              this.previous = response.data.meta.pagination.links.previous;

              this.postsWithoutFilter = response.data.data;
          })
          .catch((error) => {
              console.log(error)
          })
      },

      async currentPage(){
          const headers = { 
        "Authorization": "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6",
        "Content-Type": "application/json",
        };
          Axios.get(this.current,{headers})
          .then((response) => {
               console.log(response.data.data)
                console.log(response.data.meta.pagination)

              this.users = response.data.data;
              this.page = response.data.meta.pagination.page;
              this.total = response.data.meta.pagination.total;
              this.pages = response.data.meta.pagination.pages;
              this.current = response.data.meta.pagination.links.current;
              this.next = response.data.meta.pagination.links.next;
              this.previous = response.data.meta.pagination.links.previous;

              this.postsWithoutFilter = response.data.data;
          })
          .catch((error) => {
              console.log(error)
          })
      },

      addClick(){
          this.modalTitle="Add User";
          this.id=0;
          this.name = "";
          this.email = "";
          this.gender = "";
          this.status = "";
          console.log(this.modalTitle)
      },
      editClick(user){
          this.modalTitle="Update User";
          this.id=user.id;
          this.name=user.name;
          this.email=user.email;
          this.gender=user.gender;
          this.status=user.status ;
          console.log(this.modalTitle)
      },
      async createClick(){
    
         let name=this.name
         let email=this.email
         let gender=this.gender
         let status=this.status 
          const headers = { 
        "Authorization": "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6",
        "Content-Type": "application/json",
        };
          Axios.post('https://gorest.co.in/public/v1/users',{ name, email, gender,status },{ headers })
          .then((response) => {
              this.refreshPosts();
              console.log("create successfully")
              console.log(response.data.data.id)
              alert("create successfully : id = " + JSON.stringify(response.data.data.id))
          })
          .catch((error) => {
              console.log('errrrooooorrr' + error.response.data.data)
          })
      },
      updateClick(){
          const headers = { 
        Authorization: "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6"
        };
            Axios.put('https://gorest.co.in/public/v1/users/'+this.id,{
              id:this.id,
              name:this.name,  
              email:this.email,
              gender:this.gender, 
              status:this.status  
          },{headers: headers})
          .then((response) => {
              //this.refreshPosts();
              //this.previousChange();
              //this.nextChange();
              alert("update successfully");
              this.currentPage();
              console.log("update successfully")
              console.log(response)
          });
      },
      deleteClick(id){
          const headers = { 
        Authorization: "Bearer 9c02c2b71f36efe757f2884b8ff90c27bb955e28a993fed2ca6f7291cdc4d7f6"
        };
          if(!confirm("Are you sure?")){
              return;
          }
          Axios.delete('https://gorest.co.in/public/v1/users/'+id,{headers: headers})
          .then((response) => {
            //   this.refreshPosts();
            //   this.previousChange();
            //   this.nextChange();
            alert("delete successfully");
            this.currentPage();
              console.log(response);
              console.log("delete successfully")
          })
      },
      FilterFn(){
          var PostIdFilter=this.PostIdFilter;
          var PostNameFilter=this.PostNameFilter;

          this.users=this.postsWithoutFilter.filter(
              function(el){
                  return el.id.toString().toLowerCase().includes(
                      PostIdFilter.toString().trim().toLowerCase()
                  )&&
                  el.name.toString().toLowerCase().includes(
                      PostNameFilter.toString().trim().toLowerCase()
                  )
              }
          )
      },
  },
  mounted:function(){
      this.refreshPosts();
      this.previousChange();
      this.nextChange();
      this.currentPage();
  }
}
</script>

<style scoped>

</style>