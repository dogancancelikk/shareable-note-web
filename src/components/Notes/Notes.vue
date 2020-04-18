<template>
    <v-list subheader two-line flat>
        <v-list-item-group multiple>
            <NoteItem v-for="note in notes" :noteItem="note" v-bind:data="notes" :key="note.id"/>
        </v-list-item-group>
    </v-list>
</template>
<script>
    import NoteItem from "./NoteItem";

    export default {
        name: 'Notes',
        components: {
            NoteItem
        },
        props:['notes']
    }
</script>
<style lang="scss" scoped></style>
