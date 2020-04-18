<template>
    <v-list-item>
        <template v-slot:default="{ active, toggle }">
            <v-list-item-action>
                <v-checkbox
                        color="primary"
                        @click="toggle"
                ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
                <v-list-item-title>{{noteItem.content}}</v-list-item-title>

            </v-list-item-content>
        </template>
    </v-list-item>
</template>
<script>
    export default{
        name:'NoteItem',
        props:['noteItem'],
    }
</script>
<style lang="scss" scoped></style>
