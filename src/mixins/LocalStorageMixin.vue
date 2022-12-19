

<script>
export default {
    
    mounted(){
        this.$watch(this.field, (fieldData) => {
            localStorage.setItem(this.field, JSON.stringify(fieldData));
        })
        const data = JSON.parse(localStorage.getItem(this.field));
        if(data){
            this[this.field] = data
        }
    },

    data: () => {
        return{
            field: ''
        }
    },

    methods: {
        setLocalStorageField(field){
            this.field = field 
        }
    }
}
</script>