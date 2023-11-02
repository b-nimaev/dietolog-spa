<template>
  <div class="pagewrapper">
    <nav>
      <div class="logotype">
        <h3 class="logotype-heading">Dashboard</h3>
      </div>
      <div class="menu">
        <ul>
          <li><NuxtLink to="/">Главная</NuxtLink></li>
          <li><NuxtLink to="/statistic">Статистика</NuxtLink></li>
          <li><NuxtLink to="/promts">Промты</NuxtLink></li>
        </ul>
      </div>
    </nav>
    <NuxtPage />
  </div>
</template>

<style lang="scss">
body {
  background-color: #eee;
  color: #333
}
nav {
  display: flex;
  width: 100%;
  // border-bottom: 1px solid #0c0c0c;
  padding-bottom: 30px;
  // margin-bottom: 30px;

  .logotype-heading {
    color: #aaa
  }
}
.pagewrapper {
  padding: 30px;
  margin: 15px;
  background-color: #fff;
  border-radius: 15px;
  min-height: calc(100vh - 30px);
}

.menu {
  margin: auto 0 auto auto;
  
  ul {
    display: flex;
    margin: 0;
    padding: 0;
    list-style-type: none;
    li {
      margin-right: 15px;
      &:last-child {
        margin-right: 0;
      }
      
      a {
        text-decoration: none;
        color: #aaa
      }
    }
  }
}
</style>