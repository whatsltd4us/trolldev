<template>
  <div>
    <div
      v-for="reply in replies.data"
      :key="reply.id"
      class="mb-8 border-gray-900 border-b-[1px] border-t-[1px] ml-4 mt-4"
    >
      <div class="card card-compact">
        <div class="card-body">
          <h3 class="card-title">
            <div class="avatar">
              <div class="w-12 rounded">
                <InertiaLink
                  :href="
                    route('user-profile', {
                      id: reply.username
                    })
                  "
                >
                  <img :src="reply.avatar" />
                </InertiaLink>
              </div>
            </div>
            <div class="ml-2 text-sm">
              <InertiaLink
                :href="
                  route('user-profile', {
                    id: reply.username
                  })
                "
              >
                {{ reply.username }}
              </InertiaLink>
              <div>
                <div class="badge badge-sm badge-outline">
                  {{ reply.time }}
                </div>
              </div>
            </div>
          </h3>
          <p class="py-2">{{ reply.reply }}</p>
          <div>
            <!-- <div class="divider"></div> -->
            <div class="card-actions justify-between mt-2">
              <ReplyVote :post="reply" />
              <button
                v-if="reply.delete"
                @click="destroy(reply.id)"
                class="btn btn-ghost btn-sm"
                method="post"
                type="submit"
              >
                Delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import ReplyVote from './ReplyVote.vue'

defineProps({
  replies: Object
})

function destroy(id) {
  if (confirm('Are you sure you want to delete?')) {
    form.delete(route('reply.destroy', id))
  }
}
</script>
