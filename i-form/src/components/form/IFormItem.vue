<template>
    <div>
        <label v-if="label">{{label}}</label>
        <slot></slot>
        <p v-if="error" style="color:red;">X: {{error}}</p>
    </div>
</template>

<script>
    // 验证库
    import Schema from 'async-validator'
    
    export default {
        inject: ['form'],
        props:{
            label: {
                type: String,
                default: ''
            },
            prop:{
                type: String
            }
        },
        data(){
            return {
                error: ''
            }
        },
        mounted(){
            this.$on('validate', () => {
                this.validate()
            })
          
        },
        methods: {
           validate(){
            //    做验证
            // 获取数据
               const value = this.form.model[this.prop]
               const rule = this.form.rules[this.prop]
            
            // 进行验证
               const schema = new Schema({[this.prop]: rule})

            //    返回的是Promise对象
               return schema.validate({[this.prop]: value}, errors =>{
                   if (errors){
                       //错误
                       this.error = errors[0].message;
                       
                   }else{
                       this.error = ''
                   }
               })
           } 
        }
        
    }
</script>

<style lang="scss" scoped>
div{
    margin-top:20px;
    width:100%;
}
</style>     