<template>
    <form @submit.prevent="storePermission" @keydown="permissionForm.errors.clear($event.target.name)">
        <div class="form-group">
            <label for="">{{trans('permission.name')}}</label>
            <input class="form-control" type="text" value="" v-model="permissionForm.name" name="name" :placeholder="trans('permission.name')">
            <show-error :form-name="permissionForm" prop-name="name"></show-error>
        </div>
        <button type="submit" class="btn btn-info waves-effect waves-light pull-right">
            <span>{{trans('general.save')}}</span>
        </button>
        <button v-if="!id" type="button" class="btn btn-danger waves-effect waves-light pull-right m-r-10" @click="$emit('cancel')">{{trans('general.cancel')}}</button>
    </form>
</template>


<script>
    export default {
        data() {
            return {
                permissionForm: new Form({
                    'name' : ''
                })
            };
        },
        methods: {
            storePermission(){
                this.permissionForm.post('/api/permission')
                    .then(response => {
                        toastr.success(response.message);
                        this.$emit('completed')
                    })
                    .catch(error => {
                        helper.showErrorMsg(error);
                    });
            }
        }
    }
</script>
