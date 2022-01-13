<template>
    <table class="table is-fullwidth">
        <thead>
            <tr>
                <th v-for="head in heads" :key="head[0]+head[head.length-1]">
                    {{ head }}
                </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in data" :key="String(item[Object.keys(item)[0]])">
                <td v-for="key in Object.keys(item)" :key=key>
                    <template v-if="isImage(item[key])">
                        s
                    </template>
                    <template v-else>
                        s
                    </template>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: ['struc', 'data'],
    data() {
        return {

        }
    },
    methods: {
        isImage(text) {
            if (text.slice(0, 7) == "http://" || text.slice(0, 8) == "https://") {
                if (text.include('jpeg', 'jpg', 'png')) {
                    return true
                }
            }
            return false
        } 
    }
}
</script>