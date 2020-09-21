<template>
    <jet-action-section>
        <template #title>
            Eliminar grupo
        </template>

        <template #description>
            Eliminar permanentemente este grupo.
        </template>

        <template #content>
            <div class="max-w-xl text-sm text-gray-600">
                Una vez eliminado el grupo, todos los datos serán eliminados permanentemente. Antes de eliminarlo, por favor guarda cualquier dato o información del grupo que quieras mantener.
            </div>

            <div class="mt-5">
                <jet-danger-button @click.native="confirmTeamDeletion">
                    Eliminar grupo
                </jet-danger-button>
            </div>

            <!-- Delete Team Confirmation Modal -->
            <jet-confirmation-modal :show="confirmingTeamDeletion" @close="confirmingTeamDeletion = false">
                <template #title>
                    Eliminar grupo
                </template>

                <template #content>
                    ¿Estás seguro que quieres eliminar este grupo? Una vez eliminado, todos los datos serán eliminados permanentemente.
                </template>

                <template #footer>
                    <jet-secondary-button @click.native="confirmingTeamDeletion = false">
                        Volver
                    </jet-secondary-button>

                    <jet-danger-button class="ml-2" @click.native="deleteTeam" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                        Eliminar grupo
                    </jet-danger-button>
                </template>
            </jet-confirmation-modal>
        </template>
    </jet-action-section>
</template>

<script>
    import JetActionSection from './../../Jetstream/ActionSection'
    import JetButton from './../../Jetstream/Button'
    import JetConfirmationModal from './../../Jetstream/ConfirmationModal'
    import JetDangerButton from './../../Jetstream/DangerButton'
    import JetSecondaryButton from './../../Jetstream/SecondaryButton'

    export default {
        props: ['team'],

        components: {
            JetActionSection,
            JetButton,
            JetConfirmationModal,
            JetDangerButton,
            JetSecondaryButton,
        },

        data() {
            return {
                confirmingTeamDeletion: false,
                deleting: false,

                form: this.$inertia.form({
                    //
                }, {
                    bag: 'deleteTeam'
                })
            }
        },

        methods: {
            confirmTeamDeletion() {
                this.confirmingTeamDeletion = true
            },

            deleteTeam() {
                this.form.delete('/teams/' + this.team.id, {
                    preserveScroll: true
                });
            },
        },
    }
</script>
