<template>
        <div :class="{'active' : isFocus}">
            <!-- 实现双向数据绑定 -->
            <!-- 绑定value，实现@input -->
            <input :type="type" :value="value" @input="onInput" v-bind="$attrs" @focus="onfocus" @blur="onblur">
            
        </div>
</template>

<script>
export default{
    inheritAttrs: false,
    /*默认情况下父作用域的不被认作 props 的
    特性绑定 (attribute bindings) 将会“回退”且作
    为普通的 HTML 特性应用在子组件的根元素上。当
    撰写包裹一个目标元素或另一个组件的组件时，这可能不会总是符合预
    期行为。通过设置 inheritAttrs 到 false，这些默
    认行为将会被去掉。而通过 (同样是 2.4 新增的) 实例属性 $
    ttrs 可以让这些特性生效，且可以通过 v-bind 显性的绑定到非根元素上。*/
    data(){
        return {
            isFocus: false,
        }
    },
    props:{
        value:{
            type: String,
            default: ''
        },
        type:{
            type: String,
            default: 'text'
        }
    },
    methods: {
        onInput(e){
            //转发，把值传给老爹
            window.console.log(e)
            this.$emit('input', e.target.value)

            this.$parent.$emit('validate')
        },
        onfocus(){
            this.isFocus = true
        },
        onblur(){
            this.isFocus = false
        }
    },
}
</script>

<style lang="scss" scoped>

input {
	width:100%;
	height:40px;
    border-radius: 5px;
	border:1px solid #dbdbdb;
	outline:none;
	font-size:20px;
	text-indent:10px;
}

.active:after {
	width:calc(100% - 2px)
}
div{
    position:relative;
    
}
div::after{
	content:"";
	display:inline-block;
	width:0;
	height:2px;
	background:red;
	transition:width 1s;
	position:absolute;
	bottom:1px;
	left:1px;

}


</style>