<template>
  <section class="chat">
    <div class="chat__messages">
      <div class="chat__bubble" v-for="m in getMessages" :key="m.id" :class="{ me: m.me, other: !m.me }">
        {{(!m.me) ? `${m.user.name}:` : ''}}  {{ m.message }}
      </div>
    </div>
    <form class="chat__sender" @submit.prevent="sender">
      <el-input placeholder="Напишите сообщение" v-model="message" required>
        <el-button native-type="submit" slot="append" icon="el-icon-s-promotion"></el-button>
      </el-input>
    </form>
  </section>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'chat',
  data: () => ({
    message: null
  }),
  computed: {
    ...mapGetters(['getMessages'])
  },
  methods: {
    ...mapActions(['sendMessage']),
    sender () {
      this.sendMessage(this.message)
      this.message = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .chat{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
    &__messages{
      display: flex;
      flex-direction: column;
      width: 100vw;
      height: calc(100vh - 64px);
      overflow-y: auto;
      padding: 12px 24px;
    }
    &__sender{
      border-top: 1px solid #e2e2e2;
      display: flex;
      width: 100vw;
      height: 64px;
      padding: 12px;
    }
    &__input{
      flex: 1;
    }
    &__bubble{
      width: 90%;
      min-height: 36px;
      padding: 8px;
      border: 1px solid #e2e2e2;
      margin-bottom: 4px;
      position: relative;
      background: #00aabb;
      border-radius: 8px;
      color: white;
      &:after {
        content: '';
        position: absolute;
        top: 50%;
        width: 0;
        height: 0;
        border: 12px solid transparent;
        border-bottom: 0;
        margin-top: -10px;
      }
      &.other{
        &:after {
          left: 0;
          border-left: 0;
          border-right-color: #00aabb;
          margin-left: -12px;
        }
      }
      &.me{
        align-self: flex-end;
        text-align: right;
        &:after {
          right: 0;
          border-right: 0;
          border-left-color: #00aabb;
          margin-right: -12px;
        }
      }
    }
  }
</style>
