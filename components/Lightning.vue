<script setup>
import {onMounted} from 'vue';

onMounted(() => {

if ($slidev.nav.currentPage===$page.value){
  setTimeout(()=> {$slidev.nav.nextSlide()},1500)
}})

</script>
