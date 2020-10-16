<template>
  <briup-fulllayout title="评论">
    <div>
     
      <van-cell-group>
        <van-field v-model="form.content" placeholder="评论内容" />
      </van-cell-group>

      <van-button block type="primary" @click="submitHandler">提交</van-button>

    </div>
  </briup-fulllayout>
</template>
<script>
import {post} from '../../../http/axios'
import { mapState } from 'vuex';
import { Toast } from 'vant';
export default {
  data(){
    return {
      form:{}
    }
  },
  computed:{
    ...mapState('user',['info'])
  },
  methods:{
    submitHandler(){
      let url = "http://localhost:6677/comment/saveOrUpdate";
      this.form.customerId = this.info.id;
      post(url,this.form).then((response)=>{
        // 返回上一个页面
        this.$router.go(-1);
        // 轻提示，提示成功消息
        this.$toast.success(response.message)
        })

    }}
  }
  

</script>