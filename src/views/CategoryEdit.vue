<template>
  <div class="about">
    <h1>{{id?'编辑':'新建'}}分类</h1>
    <el-form label-width="120px" @submit.native.prevent="save">
        <el-form-item label="名称">
            <el-input v-model="model.name"></el-input>
        </el-form-item>
        <el-form-item>
            <el-button type="primary" native-type="submit">提交</el-button>
        </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
    props:{
        id:{}
    },

    data(){
        return {
            model:{}
        }
    },
    methods:{
        async save(){
             const res = this.$http.post('categories',this.model)
             .then((response)=>{
                 console.log(response)
             }).catch((error)=>{
                 console.log(error)
             })
             console.log(res)
             console.log(this.model)
             this.$router.push('/categories/list')
             this.$message({
                 type:'success',
                 message:'保存成功！'
             })
        },

        async fetch(){
            const res = await this.$http.get(`rest/admin_users/${this.id}`)
            this.model = res.data
        },

    },

    created(){
        this.id && this.fetch()
    }
}
</script>