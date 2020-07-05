<template>
    <div class="container">
        <div class="row mt-5">
            <div class="col-12">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">User Details</h3>

                        <div class="card-tools">
                            <button
                                class="btn btn-success"
                                data-toggle="modal"
                                data-target="#add-new"
                            >
                                Add New
                                <i class="fa fa-user-plus"></i>
                            </button>
                        </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body table-responsive p-0">
                        <table class="table table-hover text-nowrap">
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>User</th>
                                    <th>Email</th>
                                    <th>Phone</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>183</td>
                                    <td>John Doe</td>
                                    <td>11-7-2014</td>
                                    <td>
                                        <span class="tag tag-success"
                                            >Approved</span
                                        >
                                    </td>
                                    <td>
                                        <a href>
                                            <i class="fa fa-edit"></i>
                                        </a>
                                        <a href>
                                            <i class="fa fa-trash"></i>
                                        </a>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- /.card-body -->
                </div>
                <!-- /.card -->
            </div>
        </div>

        <!-- Modal -->
        <div
            class="modal fade"
            id="add-new"
            index="-1"
            role="dialog"
            aria-labelledby="add-new"
            aria-hidden="true"
        >
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="Add-new-user">Add User</h5>
                        <button
                            type="button"
                            class="close"
                            data-dismiss="modal"
                            aria-label="Close"
                        >
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>

                    <form @submit.prevent="createUser">
                        <div class="modal-body">
                            <div class="form-group">
                                <input
                                    v-model="form.name"
                                    type="text"
                                    name="name"
                                    placeholder="Enter Name"
                                    class="form-control"
                                    :class="{
                                        'is-invalid': form.errors.has('name')
                                    }"
                                />
                                <has-error
                                    :form="form"
                                    field="name"
                                ></has-error>
                            </div>
                            <div class="form-group">
                                <textarea
                                    v-model="form.bio"
                                    name="bio"
                                    id="bio"
                                    placeholder="Short bio for user (Optional)"
                                    class="form-control"
                                    :class="{
                                        'is-invalid': form.errors.has('bio')
                                    }"
                                ></textarea>
                                <has-error :form="form" field="bio"></has-error>
                            </div>

                            <div class="form-group">
                                <select
                                    name="type"
                                    v-model="form.type"
                                    id="type"
                                    class="form-control"
                                    :class="{
                                        'is-invalid': form.errors.has('type')
                                    }"
                                >
                                    <option value="">Select User Role</option>
                                    <option value="admin">Admin</option>
                                    <option value="user">Standard User</option>
                                    <option value="author">Author</option>
                                </select>
                                <has-error
                                    :form="form"
                                    field="type"
                                ></has-error>
                            </div>

                            <div class="form-group">
                                <input
                                    v-model="form.email"
                                    type="email"
                                    name="email"
                                    placeholder="Enter EmailAddress"
                                    class="form-control"
                                    :class="{
                                        'is-invalid': form.errors.has('email')
                                    }"
                                />
                                <has-error
                                    :form="form"
                                    field="email"
                                ></has-error>
                            </div>

                            <div class="form-group">
                                <label>Password</label>
                                <input
                                    v-model="form.password"
                                    type="password"
                                    name="password"
                                    class="form-control"
                                    :class="{
                                        'is-invalid': form.errors.has(
                                            'password'
                                        )
                                    }"
                                />
                                <has-error
                                    :form="form"
                                    field="password"
                                ></has-error>
                            </div>
                        </div>
                        <div class="modal-footer">
                            <button
                                type="button"
                                class="btn btn-secondary"
                                data-dismiss="modal"
                            >
                                Close
                            </button>
                            <button type="submit" class="btn btn-primary">
                                Create
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Form from "vform";
export default {
    data() {
        return {
            form: new Form({
                id: "",
                name: "",
                email: "",
                type: "",
                bio: "",
                password: ""
            })
        };
    },

    methods: {
        createUser() {
            this.form.post("api/users");
        }
    },
    mounted() {
        console.log("Component mounted.");
    }
};
</script>
