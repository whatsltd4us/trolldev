<script setup>
import AppLayout from '@/Layouts/AppLayout.vue'
import ProfileCard from '../Shared/ProfileCard.vue'
import Empty from '../Shared/Empty.vue'
import UserCard from '../Shared/UserCard.vue'
import SimplePagination from '../Shared/SimplePagination.vue'
import Container from '../../Pages/Shared/Container.vue'

defineProps({
  profile: Object,
  followers: Object
})
</script>
<template>
  <AppLayout title="Followers">
    <Container>
      <div class="py-10 px-4">
        <div class="mx-auto text-center">
          <ProfileCard :profile="profile" />
        </div>
      </div>

      <section class="py-12">
        <div class="max-w-7xl mx-auto px-4 lg:px-8">
          <div class="overflow-hidden sm:rounded-lg">
            <Empty v-if="followers.meta.total === 0" />

            <div class="columns-1">
              <UserCard
                class="mb-4"
                v-for="profile in followers.data"
                :key="profile.id"
                :profile="profile"
              />
            </div>

            <div class="columns-1 md:columns-1 lg:columns-1 mt-6">
              <SimplePagination v-if="followers.meta.total >= 16" :data="followers.links" />
            </div>
          </div>
        </div>
      </section>
    </Container>
  </AppLayout>
</template>
