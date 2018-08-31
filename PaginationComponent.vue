<template>
    <!--Pagination-->
    <nav aria-label="Page navigation">
        <ul v-if="current_page <= button_group + 1 || current_page > total_pages - button_group - 1" class="pagination justify-content-center">
            <!--Prev button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == 1 }">
                <a class="page-link" href="#" tabindex="-1" v-on:click="current_page -= 1">Previous</a>
            </li>
            <li v-for="n in left_group" class="page-item" v-bind:class="{'active': n == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = n;">{{ n }}</a>
            </li>
            <li v-if="total_pages > total_buttons" class="page-item">
                <i class="page-link">...</i>
            </li>
            <li v-if="total_pages > total_buttons"
                v-for="last_n in right_group" class="page-item" v-bind:class="{'active': total_pages - (right_group - last_n) == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = total_pages - (right_group - last_n)">{{ total_pages - (right_group - last_n) }}</a>
            </li>
            <!--Next Button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == total_pages }">
                <a class="page-link" href="#" v-on:click="current_page += 1">Next</a>
            </li>
        </ul>
        <ul v-else class="pagination justify-content-center">
            <!--Prev button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == 1 }">
                <a class="page-link" href="#" tabindex="-1" v-on:click="current_page -= 1">Previous</a>
            </li>
            <!-- First Page button -->
            <li class="page-item" v-bind:class="{'active': 1 == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = 1;">1</a>
            </li>
            <li v-if="total_pages > total_buttons" class="page-item">
                <i class="page-link">...</i>
            </li>
            <!-- Middle page buttons -->
            <li v-for="n in total_buttons - 2" class="page-item" v-bind:class="{'active':current_page == current_page - button_group + n }">
                <a class="page-link" href="#" v-on:click="current_page = current_page - button_group + n">{{ current_page - button_group + n }}</a>
            </li>
            <li v-if="total_pages > total_buttons" class="page-item">
                <i class="page-link">...</i>
            </li>
            <!-- Last Page button -->
            <li class="page-item" v-bind:class="{'active': total_pages == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = total_pages;">{{ total_pages }}</a>
            </li>
            <!-- Next Button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == total_pages }">
                <a class="page-link" href="#" v-on:click="current_page += 1;">Next</a>
            </li>
        </ul>
    </nav>
</template>

<script>
    export default {
        props: {
            button_group: Number,
            total_pages: Number,
            total_buttons: Number,
            value: Number
        },
        data() {
            return {
                current_page: 1,
                left_group: 0,
                right_group: 0
            }
        },
        watch: {
            current_page: function () {
                if (this.current_page == 4 || this.current_page == 5) {
                    this.left_group = 6;
                    this.right_group = 2;
                } else if (this.current_page == this.total_pages - 3 || this.current_page == this.total_pages - 4) {
                    this.left_group = 2;
                    this.right_group = 6;
                } else if(this.current_page < 4 || this.current_page > this.total_pages - 4) {
                    this.left_group = 4;
                    this.right_group = 4;
                }
                this.$emit('input', this.current_page)
            },
            value: function () {
                this.current_page = this.value;
            }
        },
        mounted: function(){
            this.left_group = this.button_group;
            this.right_group = this.button_group;
        }
    }
</script>
