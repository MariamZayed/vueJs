<template>
    <div>
        <div class="container">

            <div class="row bg-dark text-light justify-content-between p-2 align-items-baseline ">
                <button 
                @click.prevent="isBookVisible=false" 
                class="btn btn-primary">
                    Books
                </button>
                <br>
                <p style="color:yellow"><span>{{whitelist.items.length}}</span> of products</p>
                <br>
                <button 
                @click.prevent="isBookVisible=true"
                class="btn btn-primary"
                > 
                    Show Whitelist
                </button>    
                
            </div><!-- end of navbar-->


            <div v-if="isBookVisible==false" class="row justify-content-center">
                <div v-for="book in books" class="card m-3"  style="width:23rem;">
                    <img :src="book.image" class="card-img-top pt-2" :title="book.name">
                    <h4>Book Name:{{book.name}}</h4>
                    <h4>Author:{{book.author}}</h4>
                    <h4>Category:{{book.category}}</h4>
                    <h4>Price:{{formantMyCurrency(book.price)}}</h4>
                    <h4>ISBN:{{book.isbn}}</h4>
                    <h4>Number of Pages:{{book.nOfPages}}</h4>
                    <div class="card-footer d-flex justify-content-center align-item-baseline">
                        <button 
                        :disabled="existInWishList(book)"
                        @click.prevent="addToWishList(book)"
                        :class="[book.nOfPages>50?'more':'',book.nOfPages<=50?'less':'']"
                        class=" btn btn-primary">
                            Add to List
                        </button>
                    </div>
                </div>
            </div>
        </div><!-- end of books-->

        <div class="row" v-if="isBookVisible==true">
            <h3 class="text-danger text-center mt-5" v-if="whitelist.items.length==0">sorry your list is empty</h3>
            <table class="table table-striped text-center" v-if="whitelist.items.length>0">
                <thead>
                    <tr>
                        <th>ISBN</th>
                        <th>Name</th>
                        <th>Author</th>
                        <th>category</th>
                        <th>nOfPages</th>
                        <th>price</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in whitelist.items">
                        <td>{{item.isbn}}</td>
                        <td>{{item.name}}</td>
                        <td>{{item.author}}</td>
                        <td>{{item.category}}</td>
                        <td>{{item.nOfPages}}</td>
                        <td>{{formantMyCurrency(item.price)}}</td>
                        <td>
                            <a 
                            href="" 
                            class="btn btn-danger" 
                            @click.prevent="removeFromWishList(item)"
                            >
                                REMOVE
                            </a>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import books from "./../book.js";
export default {
    data:()=>({
                books:books,
                isBookVisible:false,
                whitelist:{
                    items:[]
                }
            }),
            methods:{
                addToWishList(book){
                    this.whitelist.items.push(book);
                    console.log(this.whitelist.items.length);
                },
                removeFromWishList(item) {
                    let itemIndex;
                    for(let i=0;i<this.whitelist.items.length;i++){
                        if(this.whitelist.items[i].isbn=item.isbn){
                            itemIndex=i;
                            break;
                        }
                    }
                    this.whitelist.items.splice(itemIndex, 1);
                },
                formantMyCurrency(pricing){
                    let res = Intl.NumberFormat("ar-SA", {
                        style: "currency",
                        currency: "SAR",
                        minimumFractionDigits:0,
                    }).format(pricing);
                    return res  ; 
                },
                existInWishList(findBook) {
                    return this.whitelist.items.some((el) => el.isbn == findBook.isbn);
                },
            },
            computed:{

            }
}
</script>

<style scoped>
    .more{
            color: orange;
        }

        .less{
            color: green;
        }
        .card{
            box-shadow: 1px 1px 1px 1px lightblue;
        }
        .card:hover{
            cursor: pointer;
        }
</style>
