<script>
  import { getDatabase, ref, onValue} from "firebase/database";
  import { onMount } from "svelte";

  
  
  
  $:items = [];
  //반응형 변수

const db = getDatabase();
const itemsRef = ref(db, 'items/');


  onMount(()=>{
    onValue(itemsRef, (snapshot) => {
  const data = snapshot.val();
  items = Object.values(data)
  })

});
</script>

<main>
  {#each items as item}
  <div>
    <img alt={item.title} src={item.imgUrl}>
  </div>
  <div>{item.title}</div>
  <div>{item.price}</div>
  <div>{item.place}</div>
  <div>{item.description}</div>
  {/each}
  <a href="#/write">글쓰기 페이지 라우팅</a>
</main>
