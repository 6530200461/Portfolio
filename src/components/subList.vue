<template>
    <br>
    <h2 class="text-light bg-secondary text-center pt-2">รายชื่อวิชา</h2>
    <br>
    <ul class="list-group">
        <li v-for="(sub, id) in Subject" :key="id" class="list-group-item">
            <a href="#a" @click="setShow(sub)">
                {{ sub.id }} {{ sub.name }} - ปีการศึกษา {{ sub.yr }}
            </a>

            <div v-if="sub.isShow">
                <subDetail :subId=sub.id @edit="showEdit" @delete="relode" />
            </div>
        </li>
        <div v-if="isEdit">
            {{ EditId }}
        </div>
    </ul>
</template>

<script>
import subDetail from './subDetail.vue'

export default {
    name: 'subList',
    components: { subDetail },
    data() {
        return {
            Subject: [],
            isEdit: false,
            EditId: ''
        }
    },
    mounted(){
        fetch('http://localhost:3000/Subject')
        .then(res=>res.json())
        .then(data=>this.Subject=data)
        .catch(err=>console.log(err.message))
    },
    methods: {
        setShow(theId) {
            theId.isShow = !theId.isShow
        },
        showEdit(subId) {
            this.EditId = 'มีการแก้ไข' + subId
            this.isEdit =! this.isEdit
        },
        relode(){
            this.$parent.showsubList=!this.$parent.showsubList
        },
    }

}
</script>

<style

></style>./DetailSub.vue