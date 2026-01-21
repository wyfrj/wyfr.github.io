<template>
  <div class="home">
    <section class="hero">
      <div class="hero-content">
        <div class="hero-title">
          <h1>欢迎来到我的个人博客</h1>
          <p>分享技术、生活和思考</p>
        </div>
        <router-link to="/blog" class="btn btn-primary geek-decoration">查看文章</router-link>
        <div class="hero-tech">
          <span class="tech-particle" v-for="i in 20" :key="i"></span>
        </div>
      </div>
    </section>

    <section class="features">
      <div class="container">
        <h2 class="section-title">博客特色</h2>
        <div class="features-grid">
          <div class="feature-item tech-border">
            <div class="feature-icon">
              <Book />
            </div>
            <h3>技术分享</h3>
            <p>记录学习过程中的技术心得和实践经验</p>
          </div>
          <div class="feature-item tech-border">
            <div class="feature-icon">
              <PenTool />
            </div>
            <h3>生活随笔</h3>
            <p>分享生活中的点滴感悟和美好瞬间</p>
          </div>
          <div class="feature-item tech-border">
            <div class="feature-icon">
              <Lightbulb />
            </div>
            <h3>思考感悟</h3>
            <p>记录对技术和生活的思考与感悟</p>
          </div>
        </div>
      </div>
    </section>

    <section class="latest-posts">
      <div class="container">
        <h2 class="section-title">最新文章</h2>
        <div class="post-grid">
          <div 
            v-for="post in latestPosts" 
            :key="post.id" 
            class="post-card geek-decoration"
            @click="navigateToPost(post.id)"
          >
            <h3>{{ post.title }}</h3>
            <p class="post-meta">
              {{ post.date }} · {{ post.author }}
            </p>
            <p class="post-excerpt">{{ post.content.substring(0, 100) }}...</p>
            <div class="post-tags">
              <span 
                v-for="tag in post.tags" 
                :key="tag" 
                class="tag"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRouter } from 'vue-router'
import { useBlogStore } from '../stores/blog'
import { Book, PenTool, Lightbulb } from 'lucide-vue-next'

const router = useRouter()
const blogStore = useBlogStore()

const latestPosts = computed(() => {
  return blogStore.posts.slice(0, 3)
})

const navigateToPost = (id) => {
  router.push(`/post/${id}`)
}
</script>

<style scoped>
.home {
  min-height: 100vh;
  background: var(--bg-gradient);
}

.hero {
  height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
  color: white;
  padding: 0 2rem;
  position: relative;
  overflow: hidden;
}

.hero-content {
  position: relative;
  z-index: 2;
  animation: fadeIn 1s ease-in-out;
}

.hero-title h1 {
  font-size: 4rem;
  margin-bottom: 1rem;
  font-weight: 700;
  text-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  animation: float 3s ease-in-out infinite;
}

.hero-title p {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  opacity: 0.9;
  animation: float 3s ease-in-out infinite 0.5s;
}

.hero-tech {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.tech-particle {
  position: absolute;
  width: 4px;
  height: 4px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 50%;
  animation: float 6s ease-in-out infinite;
}

.tech-particle:nth-child(1) { top: 20%; left: 10%; animation-delay: 0s; }
.tech-particle:nth-child(2) { top: 60%; left: 20%; animation-delay: 1s; }
.tech-particle:nth-child(3) { top: 40%; left: 30%; animation-delay: 2s; }
.tech-particle:nth-child(4) { top: 80%; left: 40%; animation-delay: 3s; }
.tech-particle:nth-child(5) { top: 30%; left: 50%; animation-delay: 4s; }
.tech-particle:nth-child(6) { top: 70%; left: 60%; animation-delay: 5s; }
.tech-particle:nth-child(7) { top: 50%; left: 70%; animation-delay: 0s; }
.tech-particle:nth-child(8) { top: 10%; left: 80%; animation-delay: 1s; }
.tech-particle:nth-child(9) { top: 90%; left: 90%; animation-delay: 2s; }
.tech-particle:nth-child(10) { top: 40%; left: 100%; animation-delay: 3s; }
.tech-particle:nth-child(11) { top: 20%; left: 0%; animation-delay: 4s; }
.tech-particle:nth-child(12) { top: 60%; left: -10%; animation-delay: 5s; }
.tech-particle:nth-child(13) { top: 80%; left: -5%; animation-delay: 0s; }
.tech-particle:nth-child(14) { top: 10%; left: 5%; animation-delay: 1s; }
.tech-particle:nth-child(15) { top: 30%; left: 15%; animation-delay: 2s; }
.tech-particle:nth-child(16) { top: 50%; left: 25%; animation-delay: 3s; }
.tech-particle:nth-child(17) { top: 70%; left: 35%; animation-delay: 4s; }
.tech-particle:nth-child(18) { top: 90%; left: 45%; animation-delay: 5s; }
.tech-particle:nth-child(19) { top: 40%; left: 55%; animation-delay: 0s; }
.tech-particle:nth-child(20) { top: 60%; left: 65%; animation-delay: 1s; }

.features {
  padding: 5rem 2rem;
  background: var(--bg-card);
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: var(--text-dark);
  position: relative;
  padding-bottom: 1rem;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 3px;
  background: var(--primary);
  border-radius: 3px;
  animation: scan 3s linear infinite;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.feature-item {
  text-align: center;
  padding: 2rem;
  border-radius: 15px;
  background: var(--bg-card);
  transition: all 0.3s ease;
  animation: fadeIn 0.5s ease-in-out;
}

.feature-item:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-lg);
}

.feature-icon {
  width: 80px;
  height: 80px;
  background: var(--primary-light);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  font-size: 2rem;
  color: var(--primary);
  transition: all 0.3s ease;
}

.feature-item:hover .feature-icon {
  transform: scale(1.1) rotate(360deg);
  background: var(--primary);
  color: white;
}

.feature-item h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: var(--text-dark);
}

.feature-item p {
  color: var(--text-muted);
  line-height: 1.6;
}

.latest-posts {
  padding: 5rem 2rem;
  background: var(--bg-light);
}

.post-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.post-card {
  background: var(--bg-card);
  border-radius: 15px;
  padding: 2rem;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
  cursor: pointer;
  border: 1px solid var(--border-color);
}

.post-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-md);
}

.post-card h3 {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: var(--text-dark);
  line-height: 1.4;
}

.post-meta {
  font-size: 0.9rem;
  color: var(--text-muted);
  margin-bottom: 1rem;
}

.post-excerpt {
  color: var(--text-muted);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.post-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  font-size: 0.8rem;
  padding: 0.3rem 0.8rem;
  background: var(--primary-light);
  color: var(--primary);
  border-radius: 20px;
  font-weight: 500;
}

@media (max-width: 768px) {
  .hero-title h1 {
    font-size: 2.5rem;
  }

  .hero-title p {
    font-size: 1.2rem;
  }

  .features {
    padding: 3rem 1rem;
  }

  .latest-posts {
    padding: 3rem 1rem;
  }

  .section-title {
    font-size: 2rem;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }

  .post-grid {
    grid-template-columns: 1fr;
  }
}
</style>