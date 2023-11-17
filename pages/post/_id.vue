<template>
  <article class="post">
    <header class="post-header">
      <div class="post-title">
        <h1>Post title</h1>
        <nuxt-link to="/">
          <i class="el-icon-back"></i>
        </nuxt-link> 
      </div>
      <div class="post-info">
        <small>
          <i class="el-icon-time"></i>
          {{ new Date().toLocaleString() }}
        </small>
        <small>
          <i class="el-icon-view"></i>
          42
        </small>
      </div>
      <div class="post-image">
        <img 
          src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Museumsinsel_Berlin_Juli_2021_1_%28cropped%29.jpg/1200px-Museumsinsel_Berlin_Juli_2021_1_%28cropped%29.jpg" 
          alt="post image" 
          class="post-img">
      </div>
    </header>
    <main class="post-content">
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Ad doloribus qui ab, veniam aliquid excepturi voluptates deserunt officiis quae reprehenderit eos, sed voluptatem molestias numquam. Nobis autem voluptate sed? Dolore!
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Ad doloribus qui ab, veniam aliquid excepturi voluptates deserunt officiis quae reprehenderit eos, sed voluptatem molestias numquam. Nobis autem voluptate sed? Dolore!
      </p>
    </main>
    <footer>

    </footer>
  </article>
</template>

<script>
export default {
  validate({params}) {
    return Boolean(params.id);
  }
}
</script>

<style lang="scss" scoped>
  .post{
    max-width: 600px;
    margin: 0 auto;
  }

  .post-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  .post-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5rem;
  }

  .post-image img {
    width: 100%;
    height: auto;
  }

  .post-header {
    margin-bottom: 1.5rem;
  }

  .post-content {
    margin-bottom: 2rem;
  }
</style>