<template>
    <div class="container">
			<div class="jumbotron">
				<h1>CALCULADORA</h1>
			</div>

			<hr />

			<div class="row">
				<div class="col-md-4">
					<input id="num1" type="number" class="form-control" v-model="num1" placeholder="Digite um número" />
					<div class="text-danger" v-text="errors.num1"></div>
				</div>
               
				<div class="col-md-4">
					<select id="operacao" class="form-control" v-model="operacao">
						<option value="">--Selecione uma operação</option>
						<option value="-">Subtração</option>
						<option value="+">Adição</option>
						<option value="*">Multiplicação</option>
						<option value="/">Divisão</option>
					</select>
					<div class="text-danger" v-text="errors.operacao"></div>
				</div>

				<div class="col-md-4">
					<input id="num2" type="number" class="form-control" v-model="num2" placeholder="Digite um número"/>
					<div class="text-danger" v-text="errors.num2"></div>
					
				</div>
			</div>

			<hr />

			<div class="row">
				<div class="col-md-4"></div>

				<div class="col-md-4"></div>

				<div class="col-md-4">
					<button type="button" class="btn btn-lg btn-primary pull-right" @click="calcular()">Calcular</button>
				</div>
			</div>

			<hr />

			<div class="well">
				Resultado: <input id="resultado" type="text" class="form-control" readonly v-model="resultado"/>
			</div>
			
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
			num1: '',
			operacao: '',
			num2: '',
			resultado: '',
			errors:{}
        }
        
    },
    
    methods: {

        calcular() {

			
           axios.post('http://localhost:8080/api/calculadora', {num1: this.num1, operacao: this.operacao, num2: this.num2}).then(response => {
				this.resultado = response.data;
				this.errors = {}
            }).catch(error => {
				if (error.response.status == 400) {
                    this.errors = error.response.data;
                }

			
			})
        }
    }

}
</script>