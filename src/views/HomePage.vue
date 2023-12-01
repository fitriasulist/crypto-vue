<template>
  <ion-page>
    <ion-content>
      <div class="content">
        <div class="btn">
          <ion-button @click="refreshData">
            Refresh
          </ion-button>
        </div>
            <ion-list>
              <!-- render data -->
              <ion-item v-for="item in tableData" :key="item.id" class="table-row">
                <ion-label><p>
                  Rank
                </p>{{ item.rank }}</ion-label>
                <ion-label style="text-align: left;"><p>
                  {{ item.name }}
                </p>{{ item.symbol }}</ion-label>
                <ion-label style="text-align: left;"><p>
                  USD
                </p>{{ item.price_usd }}</ion-label>
              </ion-item>
            </ion-list>

      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      tableData: []
    };
  },
  mounted() {
    this.refreshData();
  },
  methods: {
    refreshData() {
      // panggil api
      axios.get('https://api.coinlore.net/api/tickers/')
        .then(response => {
          this.tableData = response.data.data.map((item, index) => ({ 
            rank: item.rank,
            name: item.name, 
            symbol: item.symbol, 
            price_usd: Number(item.price_usd).toFixed(2) 
          }));
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    }
  }
};
</script>

<style scoped>
.content {
  max-width: 500px;
  margin: 0 auto;
  padding: auto;
}

.btn {
  display: flex;
  justify-content: center;
}

ion-list {
  margin: 0;
  padding: 0;
  border: none;
}


.table-row ion-label {
  margin: 0;
  padding: auto;
}

.table-row:nth-child(odd) ion-label {
  background-color: #eeeb47b6; 
}
.table-row:nth-child(even) ion-label {
  background-color: #eeeb47b6; 
}



.table-row {
  text-align: center;
  color: #000000;
  font-size: large;

}




</style>
