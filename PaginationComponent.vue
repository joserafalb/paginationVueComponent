<template>
    <!--Pagination-->
    <nav aria-label="Page navigation">
        <ul v-if="current_page <= button_group || current_page > total_pages - button_group" class="pagination justify-content-center">
            <!--Prev button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == 1 }">
                <a class="page-link" href="#" tabindex="-1" v-on:click="current_page -= 1">Previous</a>
            </li>
            <li v-for="n in button_group" class="page-item" v-bind:class="{'active': n == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = n;">{{ n }}</a>
            </li>
            <li v-if="total_pages > total_buttons" class="page-item">
                <i class="page-link">...</i>
            </li>
            <li v-if="total_pages > total_buttons"
                v-for="last_n in button_group" class="page-item" v-bind:class="{'active': total_pages - (button_group - last_n) == current_page }">
                <a class="page-link" href="#" v-on:click="current_page = total_pages - (button_group - last_n)">{{ total_pages - (button_group - last_n) }}</a>
            </li>
            <!--Next Button-->
            <li class="page-item" v-bind:class="{ 'disabled': current_page == total_pages }">
                <a class="page-link" href="#" v-on:click="current_page += 1; clickCallback(current_page);">Next</a>
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
                current_page: 1
            }
        },
        methods: {
            clickCallback: function (pageNum) {
                console.log(pageNum);

            }
        },
        watch: {
            current_page: function () {
                this.$emit('input', this.current_page)
            },
            value: function () {
                this.current_page = this.value;
            }

        }
    }
</script>