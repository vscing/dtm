<template>
    <div>
        <a-layout-header class="header flex">
            <div class="flex items-center logo h-16">
                <svg-icon style="width: 36px; height: 36px; margin-right: 84px;" icon-class="svg-logo" />
                <span class="text-gray-400 text-lg">DTM dashbaord {{ version }}</span>
            </div>
            <a-menu
            v-model:selectedKeys="activeMenu"
            theme="dark"
            mode="horizontal"
            :style="{ lineHeight: '64px' }"
            @select="onOpenChange"
            >
                <a-menu-item v-for="v in getMenubar.menuList" :key="v.path">{{ v.meta.title }}</a-menu-item>
            </a-menu>
        </a-layout-header>
    </div>
</template>
<script setup lang='ts'>
import { computed, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { useLayoutStore } from '/@/store/modules/layout'

const route = useRoute()
const router = useRouter()
const { getMenubar, getCurrentVersion } = useLayoutStore()
const firstRedirectPath = '/dashboard'
const version = import.meta.env.VITE_DASHBOARD_VERSION

const activeMenu = ref([route.meta.activeMenu !== firstRedirectPath ? route.meta.activeMenu : '/'])

const onOpenChange = (d:any) => {
    router.push({ path: d.key })
}
</script>

<style scoped>
.logo {
  margin-right: 20px;
}
</style>
