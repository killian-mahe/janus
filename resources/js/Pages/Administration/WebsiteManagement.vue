<template>
    <jet-action-section>
        <template #title>
            Website Management
        </template>

        <template #description>
            Check website services status and update the website version.
        </template>

        <template #content>
            <div class="grid grid-cols-2 gap-y-3">

                <div>
                    Git branch
                </div>
                <div class="italic">
                    {{ $page.props.current_branch }}
                </div>

                <div>
                    Update status
                </div>
                <div>
                    <div v-if="$page.props.commit_diff == null">
                        <span class="text-yellow-500" >Unknown</span>
                    </div>

                    <span v-else-if="$page.props.commit_diff === 0" class="text-green-500">Up to date</span>

                    <div v-else>
                        <span class="text-red-400">Not up to date.</span>
                        <br/>
                        <span class="text-sm text-gray-600">Pending commit(s) : {{$page.props.commit_diff}}</span>
                        <br/>
                        <jet-secondary-button v-if="$page.props.commit_diff > 0" :disabled="form.processing" @click="updateWebsite">Update</jet-secondary-button>
                    </div>
                    <div>
                        <span v-for="error in $page.props.errors" class="text-xs text-red-400">{{error}}</span>
                    </div>
                </div>

            </div>
        </template>
    </jet-action-section>
</template>

<script>
import JetActionSection from '@/Jetstream/ActionSection'
import JetButton from '@/Jetstream/Button'
import JetSecondaryButton from '@/Jetstream/SecondaryButton'
import JetDropdown from '@/Jetstream/Dropdown'
import JetDropdownLink from '@/Jetstream/DropdownLink'

export default {
    name: "WebsiteManagement",
    components: {
        JetActionSection,
        JetButton,
        JetSecondaryButton,
        JetDropdown,
        JetDropdownLink
    },
    data() {
        return {
            form: this.$inertia.form({})
        }
    },
    methods: {
        updateWebsite() {
            this.form.post(route('admin.update'));
        }
    }
}
</script>

<style scoped>

</style>
