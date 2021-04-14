<template>
    <div>
        <div class="container">
            <h2 class="text-center">Vue Blog 3</h2>
            <div class="row shadow-lg bg-primary pt-4 pl-4 pr-4">
                <h3 class="text-center">blog list <button class="btn btn-success pull-right" @click="openModal">add blog</button></h3>
            </div>

            <div class="shadow-lg text-center" v-for="blog in blogs">
                <h3>{{blog.title}}</h3>
                <p>{{blog.content}}</p>
            </div>
            <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
                <div class="modal-dialog modal-dialog-centered" role="document">
                    <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLongTitle">Vue Blog</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="closeModal">
                        <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body text-center">
                        <label class="text-center">Title</label>
                        <br>
                        <input type="text" class="form-control" placeholder="Title">
                        <br>
                        <label>content</label>
                        <br>
                        <textarea class="form-control" placeholder="Content"></textarea>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeModal">Close</button>
                        <button type="button" class="btn btn-primary" @click="save">Save </button>
                    </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                new_blog:{
                    title: null,
                    content: null
                },
                blogs: []
            }
        },
        mounted() {
                var __this = this;
            $('#exampleModal').on('hidden.bs.modal', function(){
                 __this.clearBlog();
                })
                __this.loadBlogs();

        },
        methods:{
            openModal(){
                $('#exampleModal').modal('show');
            },
            closeModal(){
                $('#exampleModal').modal('hide');
            },
            loadBlogs(){
                axios.get('/blog')
                .then((res)=>{
                    this.blogs = res.data.blogs;
                })
                .catch((e)=>{
                    console.error(e);
                })
                .finally(()=>{

                })

            },
            save(){
                axios.post('/blog', this.new_blog)
                .then((res)=>{
                    this.loadBlogs();
                })
                .catch((e)=>{
                    console.error(e);
                })
                .finally(()=>{
                    $('#exampleModal').modal('toggle');
                })
            },
            edit(index){

            },
            update(){

            },
            delete(){

            },
            clearBlog(){
            this.new_blog.title = null,
            this.new_blog.content = null
            }
        }
    }
</script>
