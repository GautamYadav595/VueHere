<template>
    <div class="card">
       <div class="card-header">
        <img src="https://media.istockphoto.com/id/1394440950/photo/natural-view-cosmos-filed-and-sunset-on-garden-background.jpg?s=612x612&w=0&k=20&c=eBnRobwsk2w_9MqM6bnXukIia5j-ayuMS0PeB6GHN0E=" alt="Dafault img">
       </div>
       <div class="card-title">
        <slot name="title"> Default Title</slot>
       </div>
       <div class="card-body">
            <slot name="body">This is card body containing details of the card</slot>
       </div>
       <div class="card-footer">
        <slot name="footer">
            <button>Explore more</button>
        </slot>
       </div>
    </div>
</template>

<script>
export default {
    name: 'CCard',
    data(){
        return{

        }
    }
}
</script>

<style scoped>
.card {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 16px;
    max-width: 300px;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  }
  .card-header img {
    width: 100%;
    border-radius: 8px 8px 0 0;
  }
  .card-title {
    font-size: 1.25rem;
    font-weight: bold;
    margin-top: 8px;
  }
  .card-body {
    margin-top: 8px;
  }
  .card-footer {
    margin-top: 12px;
    text-align: center;
  }
  .card-footer button {
    padding: 8px 16px;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 4px;
    cursor: pointer;
  }
  .card-footer button:hover {
    background-color: #0056b3;
  }
</style>