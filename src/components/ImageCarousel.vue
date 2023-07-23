<script setup>
  import {ref, reactive, onMounted, onUnmounted} from 'vue'

  const activeIndex = ref(0)

  const carouselItems = [
    {
      image: 'https://images.unsplash.com/photo-1664467466528-6a455ef1c98c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
      title: 'First Slide Label',
      caption: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Minima, vitae.'
    },
    {
      image: 'https://images.unsplash.com/photo-1688507383637-78f49f095269?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
      title: 'Third Slide Label',
      caption: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa ipsam laboriosam earum?'
    },
    {
      image: 'https://images.unsplash.com/photo-1658156056478-3abbe4bab958?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=904&q=80',
      title: 'Fourth Slide Label',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum augue mollis interdum.'
    },
    {
      image: 'https://images.unsplash.com/photo-1687800132770-8f1600a5849e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=928&q=80',
      title: 'Fifth Slide Label',
      caption: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa ipsam laboriosam earum?'
    },
    {
      image: 'https://images.unsplash.com/photo-1686854010079-455de3e8db41?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80',
      title: 'Sixth Slide Label',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    }
  ]

  const imageFilter = '-webkit-filter: grayscale(100%);filter: grayscale(100%);'

  const incrementActiveIndex = () =>{
    if(activeIndex.value == carouselItems.length -1){
      activeIndex.value = 0
    }
    else{
      activeIndex.value++
    }
  }

  let timerId = null;

  const startSlideShow = function(){
    timerId = setInterval(incrementActiveIndex, 3000)
  }

  const stopSlideShow = function(){
    clearInterval(timerId)
  }
 
  onMounted(() => {
    startSlideShow()
  })

  onUnmounted(() =>{
    stopSlideShow()
  })
</script>

<template>
  
  <h2 class="py-2">Image Carousel</h2>
  
  <div @mouseover="stopSlideShow" @mouseleave="startSlideShow" id="carouselExampleCaptions" class="carousel">    
    <ol class="carousel-indicators">
      <li @click="activeIndex = index" v-for="(items, index) in carouselItems" :key="index" :class="index == activeIndex?'active':''"></li>
    </ol>
    
    <div class="carousel-inner">        
      <div class="carousel-item active">           
        <img height="500" :src="carouselItems[activeIndex].image" class="d-block w-100 img img-responsive img-thumbnail" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>{{ carouselItems[activeIndex].title }}</h5>
          <p>{{ carouselItems[activeIndex].caption }}</p>
        </div>
      </div>  
    </div>    
    <a @click.prevent="0 == activeIndex ? activeIndex = (carouselItems.length) - 1 : activeIndex--" class="carousel-control-prev" href="#" role="button">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a @click.prevent="(carouselItems.length) - 1 == activeIndex ? activeIndex = 0 : activeIndex++" class="carousel-control-next" href="#" role="button">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>

  <ol class="carousel-thumnails mt-2">
    <img @click="activeIndex = index" height="50" :style="activeIndex != index?imageFilter:''" style="cursor: pointer;" class="mx-2 rounded" v-for="(thumnail, index) in carouselItems" :key="index" :src="thumnail.image" alt="">
  </ol>
  
</template>

<style>
</style>
