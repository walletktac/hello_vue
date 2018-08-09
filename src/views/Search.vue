<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import Claim from '../components/Claim';
import SearchInput from '../components/SearchInput';
import axios from 'axios';
import debounce from 'lodash.debounce';


const API = 'https://images-api.nasa.gov/search';


export default {
  name: 'Search',
  components: { Claim, SearchInput },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function() {
        axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500) 
  },
};
</script>
<style lang="scss" scoped>
  .wrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    background-image: url('../assets/')
  }
</style>
