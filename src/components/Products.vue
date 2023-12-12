<template>
    <div class="wrapper" v-if="products">
        <div class="row-wrapper">
            <div id="select-wrapper">
                <select name="prodMake" id="prodMake" v-model="selectedMake">
                    <option v-for="make in filterByMake" :key="make" :value="make">
                        {{ make }}
                    </option>
                </select>
            </div>
            <div class="search-wrapper">
                <input type="text" placeholder="Search a product by make" v-model="searchProducts" @keyup="retrieveProduct">
            </div>
        </div>
        <div class="row-wrapper" v-if="renderProducts">
            <div class="prodCard" v-for="product in renderProducts" :key="product.id">
                <div class="card-header">
                    <h3>{{ product.make }}</h3>
                </div>
                <div class="card-body">
                    <img :src="product.image" :alt="product.make" loading="lazy">
                    <p :class="{expensive : product.amount > 6300}">R{{ product.amount}}</p>
                </div>
                <div class="card-footer">
                    <a href="#" type="button">View Details</a>
                </div>
            </div>
        </div>
    </div>
    <div v-else>
        <h3>Products are out of stock.</h3>
    </div>
</template>

<script>
export default {
    name: 'ProductComp',
    data() {
        return {
            products: [
                {
                    id: 1,
                    make: "Dell",
                    spec: "Latitude-E5450 i3 5th, HDD 1TB, RAM 16GB, Operating System Windows 11 Business",
                    amount: 25000.00,
                    image: "https://i.postimg.cc/65tcMqdc/Dell-Latitude-E5450-i3-5th-GEN-1-for-business-10000.jpg"
                },
                {
                    id: 2,
                    make: "Acer",
                    spec: "Extensa 15.6 inch, SSD 256GB, RAM 8GB, Operating System Windows 10 Home",
                    amount: 6240.00,
                    image: "https://i.postimg.cc/gJKtZmp1/Acer-Extensa-15-6-inch-256-GBSSd-8-GBRAM.png"
                },
                {
                    id: 3,
                    make: "Acer",
                    spec: "Travel Mate Intel Core i5, SSD 512GB, RAM 8GB, Operating System Windows 10 Pro",
                    amount: 10000.00,
                    image: "https://i.postimg.cc/0j2WGF2j/Acer-Travel-Mate-Intel-Corei5-SSD512-8-GBRAM.png"
                },
                {
                    id: 4,
                    make: "Lenovo",
                    spec: "Idea Pad Intel Celeron, HDD 1TB, RAM 4GB, Operating System Windows 10 Home",
                    amount: 6350.00,
                    image: "https://i.postimg.cc/rwwdXLQg/Lenovo-IDea-Pad-1-TBHDD-4-GBRAM-6350.png"
                },
                {
                    id: 5,
                    make: "HP",
                    spec: "Elite Book Intel core i5, SSD 256GB, RAM 8GB, Operating System Windows 11",
                    amount: 25800.00,
                    image: "https://i.postimg.cc/7Y83v1PB/HPElite-Book-Intel-Core-i5-1135-G7-256-GBSSD-8-GB.png"
                }
            ],
            selectedMake: 'All Products',
            searchProducts: '',
            otherItem : null
        }
    },
    computed: {
        filterByMake() {
            return ['All products'].concat(Array.from(new Set(this.products.map( item => item.make))))
        },
        renderProducts() {
            return this.selectedMake.toLowerCase() != "all products" ? this.products.filter(item =>item.make.toLowerCase().includes(this.selectedMake.toLowerCase())) : this.searchProducts.toLowerCase() ? this.products.filter(item =>item.make.toLowerCase().includes(this.searchProducts.toLowerCase())) :
            this.products
        },
    }
}
</script>

<style scoped>
.row-wrapper {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
}
</style>