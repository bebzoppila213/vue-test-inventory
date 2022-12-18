
<script>
export default {

    mounted(){
        document.addEventListener('click', (event) => {
            const element = document.querySelector(this.selector)
            if(this.flag){
                if(!event.composedPath().includes(element)){
                    this.modalIsOpen = false
                    this.flag = false
                }
                
                return 
            }
            this.flag = true
        })
    },

    data: () => {
        return{
            modalIsOpen: false,
            modalSelector: '',
            flag: false,
        }
    },

    methods:{
        openModal(){
            this.modalIsOpen = true
        },

        closeModal(){
            this.modalIsOpen = false
        },

        setSelector(newSelector){
            this.selector = newSelector
        }

    }

}   
</script>