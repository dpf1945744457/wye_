<template>
  <div class="menu-wrapper">
    <template v-for="item in routes" v-if="!item.hidden&&item.children">
      <router-link v-if="item.children.length===1 && !item.children[0].children&&item.children[0].name=='dashboard'&&!item.alwaysShow" :to="item.path+'/'+item.children[0].path" :key="item.children[0].name">
        <el-menu-item :index="item.path+'/'+item.children[0].path" :class="{'submenu-title-noDropdown':!isNest}">
          <icon :scale="2" v-if="item.children[0].meta&&item.children[0].meta.icon" :name="item.children[0].meta.icon"></icon>
          <span v-if="item.children[0].meta&&item.children[0].meta.title">{{item.children[0].meta.title}}</span>
        </el-menu-item>
      </router-link>

      <el-submenu v-else :index="item.name||item.path" :key="item.name">
        <template slot="title">
          <icon :scale="2" v-if="item.meta&&item.meta.icon" :name="item.meta.icon"></icon>
          <span v-if="item.meta&&item.meta.title">{{item.meta.title}}</span>
        </template>

        <template v-for="child in item.children" v-if="!child.hidden">
          <sidebar-item :is-nest="true" class="nest-menu" v-if="child.children&&child.children.length>0" :routes="[child]" :key="child.path"></sidebar-item>
          <router-link v-else :to="item.path+'/'+child.path" :key="child.name">
            <el-menu-item :index="item.path+'/'+child.path">
              <icon :scale="2" v-if="child.meta&&child.meta.icon" :name="child.meta.icon"></icon>
              <span v-if="child.meta&&child.meta.title">{{child.meta.title}}</span>
            </el-menu-item>
          </router-link>
        </template>
      </el-submenu>

    </template>
  </div>
</template>


<script>
// import { mapActions } from "vuex";
export default {
  name: "SidebarItem",
  props: {
    routes: {
      type: Array
    },
    isNest: {
      type: Boolean,
      default: false
    }
  },
  computed: {},
  methods: {
    // ...mapActions({
    //   GetMenuFunctionList: "GetMenuFunctionList" // map `this.add()` to `this.$store.dispatch('increment')`
    // })
  },
  mounted() {
  	console.log("routes",this.routes)
  },
  watch: {
    // $route(data) {
    //   let menuCode = data.meta.name;
    //   this.GetMenuFunctionList(menuCode)
    //     .then(res => {})
    //     .catch(error => {});
    // }
  }
};
</script>

 