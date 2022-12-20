
<template>
  <div>
    <Header />
    <div id="body">
      <h1> Formulário de Cadastro </h1>
      <Form />
      <Cadastrados/>
      <FilterData/>

    </div>
  </div> 
</template>

<style scoped>
.inv {
    background-color: transparent;
}

* {
  margin: 0;
  padding: 0;
  background-color: lightcyan;
  justify-content: center;
  height: 2800px;
}

h1 {
  background-color: transparent;
  margin-top: 40px;

}

  #body {
    justify-content: flex-start;
    place-items: center;
    display: flex;
    flex-direction: column;
    width: 700px;
    height: 800px;
    margin-top: 75px;
    border: 1px solid;
    margin-left: auto;
    margin-right: auto;
    background-color: rgba(97, 191, 235, 0.986);
    border-radius: 20px;

  }

</style>

<script>
    import Header from './components/Header.vue';
    import Form from './components/Form.vue';    
    import Cadastrados from './views/Cadastrados.vue';
    import FilterData from './components/Filterdata.vue';
    

  export default {
    name:'App',
    components: {
      Header,
      Form,
      Cadastrados,
      FilterData
    }
  }
</script>