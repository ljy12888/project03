<template>
  <div class="page_container">
    <span v-show="isLoading" class="loading_spinner">로딩중...</span>
    <section>
      <h1 class="dog_title">멍이사전</h1>
      <form action="#" class="dog_seacrh_form" @submit.prevent="submit">
        <label for="dog_search"
          ><svg
            xmlns="http://www.w3.org/2000/svg"
            height="1em"
            viewBox="0 0 512 512"
          >
            <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
            <path
              d="M416 208c0 45.9-14.9 88.3-40 122.7L502.6 457.4c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L330.7 376c-34.4 25.2-76.8 40-122.7 40C93.1 416 0 322.9 0 208S93.1 0 208 0S416 93.1 416 208zM208 352a144 144 0 1 0 0-288 144 144 0 1 0 0 288z"
            /></svg
        ></label>
        <input type="text" id="dog_search" />
      </form>
      <ul class="dog_ul">
        <li class="dog_items" v-for="(dog, i) in dogBreedInfo" :key="dog.id">
          <router-link :to="'/dog/breed/detail/' + (i + 1)">
            <img
              class="dog_image"
              :src="require(`@/assets/db_dog_image/${dog.image}`)"
            />
            <p class="dog_name">
              {{ dog.name }} <br />
              ({{ dog.ko_name }})
            </p>
          </router-link>
        </li>
      </ul>
    </section>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      dogBreedInfo: [],
      isLoading: true
    }
  },
  async mounted() {
    this.isLoading = true
    try {
      const response = await axios.get('http://localhost:3000/dog/breed')
      if (response.status === 200) {
        this.dogBreedInfo = response.data
        this.isLoading = false
      }
    } catch (error) {
      console.error('dog 정보를 받아오는 중 에러가 발생하였습니다:', error)
    }
  }
}
</script>
<style scoped>
* {
  margin: 0px;
  padding: 0px;
}
.dog_title {
  margin-top: 20px;
  text-align: center;
}
ul,
ol,
li {
  list-style: none;
}

a {
  text-decoration: none;
}

/*컨테이너*/
.page_container {
  animation: appear 1s 1 ease-in-out;
}

@keyframes appear {
  from {
    opacity: 0;
    visibility: hidden;
  }
}

/* 검색창 폼 */
.dog_seacrh_form {
  max-width: 400px;
  background-color: white;
  box-shadow: 0 0 5px 2px rgb(220, 220, 220);
  border-radius: 50px;
  margin: 2rem auto;
  padding: 12px;
}

/* 검색창 input*/
.dog_seacrh_form input {
  max-width: 300px;
  width: 100%;
  padding: 12px;
  border: none;
}

.dog_seacrh_form input:focus {
  outline: none;
}

/* 검색창 input 라벨 */

.dog_seacrh_form label {
  font-size: 1.25rem;
}

.dog_seacrh_form label svg {
  margin-top: 10px;
}

section {
  height: 100%;
  top: 0px;
  left: 0px;
}

.dog_ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.dog_image {
  width: 230px;
  height: 230px;
  border-bottom: 4px solid rgb(198, 111, 17);
}

.dog_items {
  box-shadow: 0 0 5px 2px rgb(223, 222, 222);
  margin: 10px;
  text-align: center;
  padding: 1px 0;
}

.dog_items .dog_name {
  font-size: 15px;
  height: 35px;
  padding: 0px 10px 10px 0;
  color: rgb(0, 0, 0);
}
.loading_spinner {
  font-size: 3rem;
  position: fixed;
  left: 50%;
  top: 0;
  line-height: 500px;
  color: white;
  text-shadow: 2px 2px 1px rgba(0, 0, 0, 0.712);
  font-weight: 900;
  transform: translate(-50%);
  width: 100%;
  text-align: center;
  height: 100vh;
  background: rgba(128, 128, 128, 0.407);
}
</style>
