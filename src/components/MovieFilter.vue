<template>
    <div id="movie-filter">
        <h2>Filter results</h2>
        <h3>By time of day</h3>
        <div class="filter-group">
            <check-filter v-for="time in times" category="time" v-bind:title="time" v-on:check-filter="checkFilter"></check-filter>
        </div>
        <h3>By genre</h3>
        <div class="filter-group">
            <check-filter v-for="genre in genres" category="genre" v-bind:title="genre" v-on:check-filter="checkFilter"></check-filter>
        </div>
    </div>
</template>
<script>
    import genres from '../util/genres';
    import times from '../util/times';
    import CheckFilter from './CheckFilter.vue';

    export  default {
        data() {
            return {
                genres,
                times
            }
        },
        methods: {
            checkFilter(category, title, checked) {
                this.$emit('check-filter', category, title, checked);
            }
        },
        components: {
            'check-filter': {
                data() {
                    return {
                        checked: false
                    }
                },
                props: ['title'],
                template: `<div :class="{'check-filter':true, active: checked}" v-on:click="checkFilter">
                    <span class="checkbox"></span>
                    <span class="check-filter-title">{{title}}</span>
                    </div>`,
                methods: {
                    checkFilter() {
                        this.checked = !this.checked;
                        this.$emit('check-filter', 'genre', this.title, this.checked);
                    }
                }

            }
        }
    }


</script>