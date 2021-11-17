<template>
<body>  
  <div class="container">
<h1 style="color:black; font-weight: bold; font-size: 60px;">Lista de Tarefas</h1>


<input v-model="tarefa" type="text" placeholder="Digitar tarefa" class="form-control">
<button style="margin-top:15px" class="btn" @click="enviarTarefa">+</button>

<table class="table table-bordered mt-5" style="border: 3px solid white; background: black; color: white; font-size: 25px">
  <thead>
    <tr style="border: 3px solid white">
      <th scope="col" style="border: 3px solid white" >Tarefa</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center" style="border: 3px solid white">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index" style="border: 3px solid white">
      <td style="border: 3px solid white">
        <span :class="{'tarefaCompleta': task.status === 'Feito'}">{{task.task}}</span>
        </td>
      <td style="width: 150px">
        <span class="pointer" @click="mudarStatus(index)"
          :class="{'text-danger': task.status === 'Fazer',
          'text-warning': task.status === 'Fazendo',
          'text-success': task.status === 'Feito'
          }"
          >
        {{task.status}}
      </span>
      </td>
      <td style="border: 3px solid white"> 
<div class="text-center" @click="editarTarefa (index)">
<span class="fa fa-pen"></span>
</div>
      </td>
      <td>
<div class="text-center" @click="deletarTarefa (index)">
<span class="fa fa-trash"></span>
</div>
      </td>
    </tr>
  </tbody>
</table>
</div>
</body>
</template>

<script>
export default {
  name: 'ListaApp',
  props: {
    msg: String
  },

  data(){
    return{
      tarefa: '',
      tarefaEditada: null,
      statusAtual: ['Fazer', 'Fazendo', 'Feito'],
      tasks: [
        {
        task: 'Tarefa-Editável',
        status: 'Fazer'
        },
        {
        task: 'Tarefa-Editável',
        status: 'Fazer'
        }
      ]
    }
  },

  methods:{
    enviarTarefa(){
      if(this.tarefa.length === 0) return;

if(this.tarefaEditada === null){

      this.tasks.push({
        task: this.tarefa,
        status: 'Fazer'
      });
} else {
  this.tasks[this.tarefaEditada].task = this.tarefa;
  this.tarefaEditada = null;
}
      this.tarefa = '';
    },

    deletarTarefa(index){
      this.tasks.splice(index, 1);
    },

    editarTarefa(index){
      this.tarefa = this.tasks[index].task;
      this.tarefaEditada = index;
    },

    mudarStatus(index){
      let novoIndex = this.statusAtual.indexOf(this.tasks[index].status)
      if(++novoIndex > 2) novoIndex = 0;
      this.tasks[index].status = this.statusAtual[novoIndex];
    }
  }
};

</script>


<style scoped>
.container{
  margin-top: 200px;
  text-align: center;
  font-family: sans-serif;
  font-size: 30px;
  border: 1px solid rgb(0, 0, 0);
  padding: 50px;
  border-radius: 10px;
}

.form-control{
  padding: 15px;
  border-radius: 16px 0px 16px 0px;
  box-shadow: 5px 1px 5px 1px;
  font-size: 40px;
}

.btn{
  margin-left: 30px;
  padding: 15px;
  font-size: 30px;
  margin-bottom: 10px;
  background: hsl(2, 83%, 55%);
  cursor:pointer;
}

.btn:hover{
  background: rgb(230, 103, 92);
}

.text-center{
  cursor:pointer;
}

.pointer{
  cursor:pointer;
}

.tarefaCompleta{
  color: green;
  font-weight: bold;
}

body{
  width: 100%;
}

</style>
