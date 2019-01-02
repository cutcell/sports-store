<template>
    <div class="row mt-2">
        <div class="col form-group">
            <select class="form-control" @change="changePageSize">
                <option value="4">4 per page</option>
                <option value="8">8 per page</option>
                <option value="12">12 per page</option>
            </select>
        </div>
        <div class="text-right col">
            <div v-if="pageCount > 1" class="text-right">
                <div class="btn-group mx-2">
                    <button v-for="pn in pageNumbers" :key="pn"
                        class="btn btn-secondary"
                        :class="{ 'btn-primary': pn === currentPage }"
                        @click="setCurrentPage(pn)">
                    {{ pn }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import { mapState, mapGetters, mapMutations } from 'vuex';

export default {
    computed: {
        ...mapState(['currentPage']),
        ...mapGetters(['pageCount']),
        pageNumbers() {
            return [...Array(this.pageCount + 1).keys()].slice(1)
        }
    },
    methods: {
        ...mapMutations(['setCurrentPage', 'setPageSize']),
        changePageSize($event) {
            this.setPageSize(Number($event.target.value));
        }
    }
}
</script>
