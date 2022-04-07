<template>
    <div class="jobList">
        <p class="orderTitle">Ordered by <span>{{order}}</span></p>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{job.title}} in {{job.location}}</h2>
                <div class="salary">
                    <p>{{job.salary}} $</p>
                </div>
                <div class="description">
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Deleniti necessitatibus voluptatem perferendis nam quasi recusandae voluptatibus reiciendis nisi non, rerum temporibus commodi nihil mollitia culpa maiores soluta vitae veniam magnam.</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import Job from '@/types/job';
import { OrderTerm } from '@/types/orderTerm';
import { defineComponent, PropType } from 'vue';

export default defineComponent({
    props: {
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },

    computed: {
        orderedJobs() {
            return [...this.$props.jobs].sort((a: Job, b: Job) => {
                return a[this.$props.order] > b[this.$props.order] ? 1 : -1;
            });
        }
    }
});
</script>

<style lang="scss" scoped>
.jobList{
    max-width: 1000px;
    margin: 40px auto;
    padding-left: 20px;
    padding-right: 20px;
    .orderTitle{
        text-align: center;
        span{
            font-weight: bold;
            font-size: 20px;
        }
    }
    ul{
        padding: 0;
        li{
            list-style-type: none;
            background: #fff;
            padding: 16px;
            margin: 16px 0;
            border-radius: 4px;
            h2{
                margin: 0 0 10px;
                text-transform: capitalize;
            }
            .salary{
                display: flex;
                img{
                    width: 30px;
                }
                p{
                    color: #17bf66;
                    font-weight: bold;
                    margin: 10px 4px;
                }
            }
        }
    }
    .list-move{
        transition: all 1s;
    }
}
</style>