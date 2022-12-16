
<script>
export default {
    data:() => {
        return{
            elementIsOpen: false
        }
    },

    methods:{
        closeElement(){
            this.elementIsOpen = false
        },

        openElement(){
            this.elementIsOpen = true
        }
    }
}
</script>