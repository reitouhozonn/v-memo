<template>
    <div>
        <header>
            my-memo
        </header>
    <main>
        <p class="info-line">All: {{ totalCardCount }} tasks</p>
        <draggable class="list-index"
            :list="lists"
            @end="movingList">
            <list v-for="(item,index) in lists"
                :key="item.id"
                :title="item.title"
                :cards="item.cards"
                :listIndex= "index"
                @change="movingCard"
            />
        <list-add />
        </draggable>
    </main>
    </div>
</template>

<script>
import ListAdd from './ListAdd'
import List from './List'
import { mapState } from 'vuex'
import draggable from "vuedraggable";


export default {
    components: {
        ListAdd,
        List,
        draggable,
    },
    computed: {
        ...mapState([
            'lists'
        ]),
        totalCardCount() {
            return this.$store.getters.totalCardCount
        }
    },
    methods: {
        movingCard() {
            this.$store.dispatch('updateList', {lists: this.lists})
        },
        movingList() {
            this.$store.dispatch('updateList', {lists: this.lists})
        },
    },
}
</script>
