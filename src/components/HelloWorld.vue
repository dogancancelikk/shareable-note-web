<template>
    <v-container class="main-content">
        <div class="list-container">
            <div class="list-container__header">
                <div class="list-container__header__list-name">{{listName}}</div>
                <div class="list-container__header__new-list-button-container">
                    <v-btn large color="primary" class="new-list-button">Add List Item</v-btn>
                </div>
            </div>
            <div class="list-container__content">
                <div class="list-container__content__empty-list" v-if="false">
                    <v-img
                            alt="Share Logo"
                            class="shrink mr-2"
                            contain
                            src="../assets/empty_list.png"
                            transition="scale-transition"
                            width="280"
                    />
                    <div class="list-container__content__empty-list__text">
                        Start Adding Items
                    </div>
                </div>
                <div class="list-container__content__list" v-if="true">
                    <Notes :notes="notes"/>
                </div>
            </div>

        </div>
    </v-container>
</template>

<script>
    //-M4fPQcMZ3TEWmNF9_Zx
    import Notes from '../components/Notes/Notes'
    import {db} from "../db";
    export default {
        name: 'HelloWorld',
        components: {
            Notes,
        },
        data: () => ({
            notes: [],
            listName: ''
        }),
        mounted() {
            const path = window.location.pathname.split('/');
            const id = path[path.length-1];
            let listsRef = db.ref('lists/' + id)

            listsRef.on('value', (snapshot) => {
                this.listName = snapshot.val().title;
                const _notes = Object.values(snapshot.val().notes);
                _notes.forEach((note, key) => {
                    const noteItem = {}
                    noteItem.id = key;
                    noteItem.content = note.content;
                    this.notes.push(noteItem);
                })
            })
        }

    }
</script>
<style lang="scss" scoped>
    .main-content {
        display: flex;
        justify-content: center;
        overflow-y: hidden;
    }

    .list-container {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        width: 50%;
        height: 100vh;
        margin-top: 3%;
        overflow-y: hidden;

        &__header {
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            width: 100%;
            flex-basis: 15%;
            justify-content: space-around;
            overflow: hidden;

            &__list-name {
                font-size: 1.75rem;
                width: 100%;
                justify-content: flex-start;
                color: #707070;
                text-overflow: ellipsis;
            }

            &__new-list-button-container {
                display: flex;
                width: 100%;
                height: 100%;
                align-items: center;

                .new-list-button {
                    width: 100%;
                    height: 100%;
                }
            }

        }

        &__content {
            display: flex;
            flex-direction: column;
            width: 100%;
            height: 100%;

            &__empty-list {
                display: flex;
                justify-content: center;
                align-items: center;
                height: 70%;
                flex-direction: column;

                &__text {
                    color: rgba(0, 0, 0, .54);
                    display: flex;
                    justify-content: center;
                    font-size: 20px;
                    font-weight: bold;
                }
            }
        }
    }

    @media only screen and (max-width: 600px) {
        .list-container {
            width: 80%;
        }
    }
</style>
