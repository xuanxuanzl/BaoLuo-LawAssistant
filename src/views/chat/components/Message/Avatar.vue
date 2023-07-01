<script lang="ts" setup>
import { computed } from 'vue'
import { NAvatar } from 'naive-ui'
import { useUserStore } from '@/store'
import { isString } from '@/utils/is'

interface Props {
  image?: boolean
}
defineProps<Props>()

const userStore = useUserStore()

const avatar = computed(() => userStore.userInfo.avatar)
</script>

<template>
  <template v-if="image">
    <NAvatar v-if="isString(avatar) && avatar.length > 0" :src="avatar" />
    <NAvatar v-else round />
  </template>
	<span class="text-gray-700 dark:text-gray-400">
		<svg viewBox="0 0 200 200" width="2em" height="2em">
			<circle cx="100" cy="100" r="90" stroke="#555" stroke-width="30" fill="none" />
			<path d="M100 40 Q 120 100 100 160 M100 40 Q 80 100 100 160" stroke="#000" stroke-width="30" fill="none" />
			<path d="M100 60 Q 110 100 100 140 M100 60 Q 90 100 100 140" stroke="#000" stroke-width="30" fill="none" />
			<path d="M100 80 Q 100 100 100 120" stroke="#000" stroke-width="30" fill="none" />
			<circle cx="100" cy="100" r="40" fill="#C4C4C4" />
			<circle cx="100" cy="100" r="20" fill="#F5F5F5" />
		</svg>
	</span>
</template>
