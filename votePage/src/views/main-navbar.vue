<template>
  <nav class="site-navbar" :class="'site-navbar--' + navbarLayoutType">
    <div class="site-navbar__header">
      <h1 class="site-navbar__brand" @click="$router.push({ name: 'home' })">
        <a class="site-navbar__brand-lg" href="javascript:;">
          <img
            style="width: 57%;margin-top: -10px;float: left;"
            src="~@/assets/img/logo.png"
            alt="logo"
          />
          <span style="color:#cc9844;float: left; margin-left: -22px;">幸福亿家</span>
        </a>
      </h1>
    </div>
    <div class="site-navbar__body clearfix">
      <el-menu class="site-navbar__menu site-navbar__menu--right" mode="horizontal">
        <el-menu-item class="site-navbar__avatar" index="3">
          <el-dropdown :show-timeout="0" placement="bottom">
            <span class="el-dropdown-link">
              <img src="~@/assets/img/avatar.png" :alt="userName" />
              {{ userName }}
            </span>
            <el-dropdown-menu slot="dropdown">
              <!-- <el-dropdown-item @click.native="updatePasswordHandle()">修改密码</el-dropdown-item> -->
              <el-dropdown-item @click.native="logoutHandle()">去客户端</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-menu-item>
      </el-menu>
    </div>
    <!-- 弹窗, 修改密码 -->
    <update-password v-if="updatePassowrdVisible" ref="updatePassowrd"></update-password>
  </nav>
</template>

<script>
import UpdatePassword from './main-navbar-update-password'
// import { clearLoginInfo } from '@/utils'
export default {
  data () {
    return {
      updatePassowrdVisible: false
    }
  },
  components: {
    UpdatePassword
  },
  computed: {
    navbarLayoutType: {
      get () { return this.$store.state.common.navbarLayoutType }
    },
    sidebarFold: {
      get () { return this.$store.state.common.sidebarFold },
      set (val) { this.$store.commit('common/updateSidebarFold', val) }
    },
    mainTabs: {
      get () { return this.$store.state.common.mainTabs },
      set (val) { this.$store.commit('common/updateMainTabs', val) }
    },
    userName: {
      get () { return this.$store.state.user.name }
    }
  },
  methods: {
    // 修改密码
    updatePasswordHandle () {
      // this.updatePassowrdVisible = true
      // this.$nextTick(() => {
      //   this.$refs.updatePassowrd.init()
      // })
    },
    // 去客户端
    logoutHandle () {
      this.$router.push({ name: 'home' })
    }
  }
}
</script>
