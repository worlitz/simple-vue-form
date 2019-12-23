<template>
    <div class="form-input">
        <h2>IForm</h2>
        <IForm :model="model" :rules="rules" ref="loginForm">
            <IFormItem label="用户名" prop="username">
     
                  <IInput v-model="model.username" placeholder="用户名" ></IInput>              
    

            </IFormItem>
            <IFormItem label="密码" prop="password" >
         
                    <IInput type="password" v-model="model.password" placeholder="密码"></IInput>
      
            </IFormItem>
            <IFormItem>
                <div @click="submit" class="button"><span>点击提交</span></div>
            </IFormItem>
        </IForm>

    </div>
</template>

<script>
    import IInput from '@/components/form/IInput.vue';  
    import IFormItem from '@/components/form/IFormItem.vue';
    import IForm from '@/components/form/IForm.vue';

    
    export default {
        components:{
            IInput,
            IFormItem,
            IForm
            
        },
        data(){
            
            return {
                model: {username: '', passowrd: 'xxx'},
                rules: {
                    username:[{required: true, message: "用户名必填"}], 
                    password: [{required: true, message:"密码必填"}]
                }
            }
        },
        methods: {

            submit(){
                this.$refs.loginForm.validate(isValidate => {
                    if (isValidate){
                        alert("输入验证通过，在这里进入登陆处理")

                    }else{
                        alert("输入验证失败")
                    }
                })
            }
            ,
 
        },
    }
</script>

<style lang="scss" scoped>
.form-input {
    position: relative;
    border: 1px solid #ccc; 
    width: 50vw;
    height: 50vh;
    top: 25vh;
    left: 25vw;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: column;
    padding:20px;
    
}

.button{
    background-image: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
    width: 10vh;
    height: 3vh;
    min-height: 30px;
    min-width: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    overflow: hidden;
    margin: 0 0.8rem;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2), 0 3px 8px rgba(0, 0, 0, 0.1);
    transition: all 0.3s cubic-bezier(0, 0.22, 0.3, 1);
}
.button span {
  color: #fff;
  font-size: 1rem;
  z-index: 10;
  text-transform: uppercase;
  letter-spacing: 2px;
}

</style>