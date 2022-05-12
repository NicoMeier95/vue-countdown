<template>
    <div v-if="loaded">
        <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
            <h5 v-if="!expired">Camino a Qatar 2022</h5>
            <h5 v-else>¡¡Vamos Argentina!!</h5> 
        </section>
        <section class="flex text-6xl justify-center content-center">
            <div class="days mr-2 relative">
                {{mostrarDias}}
                <div class="label text-sm absolute bottom-0">Días</div>        
            </div>
            <span class="leading-snug">:</span>
            <div class="hours mx-2 relative">
                {{mostrarHoras}}
                <div class="label text-sm absolute bottom-0">Horas</div>
            </div>
            <span class="leading-snug">:</span>
            <div class="minutes mx-2 relative">
                {{mostrarMinutos}}
                <div class="label text-sm absolute bottom-0">Minutos</div>
            </div>
            <span class="leading-snug">:</span>
            <div class="seconds mx-2 relative">
                {{mostrarSegundos}}
                <div class="label text-sm absolute bottom-0">Segundos</div>
            </div>

        </section>
        
    </div>
</template>

<script>
    export default {
        name: 'Counter',
        props:['año','mes','dia','hora','minuto','segundo','milisegundo'],
        data() {
            return {
                mostrarDias : 0,
                mostrarHoras : 0,
                mostrarMinutos : 0,
                mostrarSegundos : 0,
                loaded: false,
                expired : false
            }
        },
        computed:{
            _segundos: () => 1000,
            _minutos(){
                return this._segundos * 60
            },
            _horas(){
                return this._minutos * 60
            },
            _dias(){
                return this._horas * 24
            },
            end(){
                return new Date(
                this.año,
                this.mes,
                this.dia,
                this.minuto,
                this.segundo,
                this.milisegundo,
                ) 
            }
        },
        methods:{
            formatNum: num => (num <10? '0' + num : num),
            showRemaining(){
                const timer = setInterval(()=>{
                    const now = new Date();
                    const end = new Date(2022, 10 , 22,7,0,0);
                    const distance = end.getTime() - now.getTime();

                    if(distance < 0){
                        clearInterval(timer);
                        this.expired = true;
                        this.loaded = true;
                        return
                    }

                    const dias = Math.floor((distance / this._dias));
                    const horas = Math.floor((distance % this._dias)/this._horas);
                    const minutos = Math.floor ((distance % this._horas)/this._minutos);
                    const segundos = Math.floor((distance % this._minutos)/this._segundos);

                    this.mostrarDias = this.formatNum(dias);
                    this.mostrarHoras = this.formatNum(horas);
                    this.mostrarMinutos = this.formatNum(minutos);
                    this.mostrarSegundos = this.formatNum(segundos);
                    this.loaded = true;

                },1000)
            }
        },
        mounted() {
            this.showRemaining();
        },
    }
</script>

<style scoped>
.seconds{
    max-width: 60px;
}
</style>