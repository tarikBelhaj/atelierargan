---
layout: default
title: "Tous nos articles"
permalink: /articles/
description: "Découvrez tous nos articles de blog sur l'huile d'argan, la beauté naturelle et les soins authentiques"
---

<div class="articles-page">
  <div class="container">
    <!-- Hero Articles -->
    <section class="articles-hero">
      <h1 class="page-title fade-in">
        Découvrez tous nos <span class="highlight">articles</span>
      </h1>
      <p class="page-subtitle fade-in">
        Explorez notre collection complète d'articles sur l'huile d'argan, 
        les rituels beauté et les secrets de la cosmétique naturelle marocaine.
      </p>
    </section>

    <!-- Filtres et recherche -->
    <section class="articles-filters fade-in">
      <div class="filter-container">
        <div class="search-box">
          <input type="text" id="search-articles" placeholder="Rechercher un article..." class="search-input">
          <span class="search-icon">🔍</span>
        </div>
        
        <div class="category-filters">
          <button class="filter-btn active" data-filter="all">Tous les articles</button>
          <button class="filter-btn" data-filter="soins-visage">Soins visage</button>
          <button class="filter-btn" data-filter="soins-cheveux">Soins cheveux</button>
          <button class="filter-btn" data-filter="diy-recettes">DIY & Recettes</button>
          <button class="filter-btn" data-filter="bien-etre">Bien-être</button>
        </div>
      </div>
    </section>

    <!-- Articles Grid -->
    {% if site.posts == empty %}
      <div class="no-articles">
        <div class="empty-state">
          <div class="empty-icon">📝</div>
          <h3>Aucun article pour le moment</h3>
          <p>Notre équipe travaille actuellement sur de nouveaux contenus passionnants. Revenez bientôt !</p>
        </div>
      </div>
    {% else %}
      <section class="articles-content">
        <div class="articles-stats fade-in">
          <p><strong>{{ site.posts.size }}</strong> article{% if site.posts.size > 1 %}s{% endif %} au total</p>
        </div>

        <div class="articles-grid" id="articles-container">
          {% assign posts_all = site.posts | sort: "date" | reverse %}
          {% for post in posts_all %}
            <article class="article-card fade-in" 
                     data-category="{{ post.tags.first | slugify | default: 'general' }}"
                     data-title="{{ post.title | downcase }}"
                     data-content="{{ post.description | default: post.excerpt | strip_html | downcase }}">
              
              <a class="article-thumb" href="{{ post.url | relative_url }}">
                {% if post.image %}
                  <img src="{{ post.image | relative_url }}" 
                       alt="{{ post.image_alt | default: post.title }}"
                       loading="lazy">
                {% else %}
                  <div class="thumb-placeholder" aria-hidden="true">ARGAN</div>
                {% endif %}
                
                {% if post.tags and post.tags.first %}
                  <span class="article-tag">{{ post.tags.first }}</span>
                {% endif %}
              </a>

              <div class="article-body">
                <h2 class="article-title">
                  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                </h2>

                <div class="article-meta">
                  <time datetime="{{ post.date | date_to_xmlschema }}">
                    {{ post.date | date: "%d %B %Y" }}
                  </time>
                  {% if post.author %}
                    <span>• {{ post.author }}</span>
                  {% endif %}
                  {% if post.reading_time %}
                    <span class="read-time">⏱ {{ post.reading_time }} min</span>
                  {% endif %}
                </div>

                <p class="article-excerpt">
                  {{ post.description | default: post.excerpt | strip_html | truncatewords: 28 }}
                </p>

                <a class="article-read" href="{{ post.url | relative_url }}">
                  Lire la suite →
                </a>
              </div>
            </article>
          {% endfor %}
        </div>

        <!-- Load More Button -->
        <div class="load-more-container" id="load-more-container" style="display: none;">
          <button class="btn load-more-btn" id="load-more-btn">
            Charger plus d'articles
          </button>
        </div>

        <!-- No Results -->
        <div class="no-results" id="no-results" style="display: none;">
          <div class="empty-state">
            <div class="empty-icon">🔍</div>
            <h3>Aucun article trouvé</h3>
            <p>Essayez de modifier vos critères de recherche ou de filtrage.</p>
            <button class="btn btn-secondary" onclick="resetFilters()">Réinitialiser</button>
          </div>
        </div>
      </section>
    {% endif %}
  </div>
</div>

<style>
/* Styles pour la page articles */
.articles-page {
  padding-top: 6rem; /* Compensation header fixe */
}

.articles-hero {
  text-align: center;
  padding: 4rem 0 2rem;
}

.page-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: var(--font-weight-bold);
  margin-bottom: 1.5rem;
  color: var(--dark);
}

.page-subtitle {
  font-size: 1.2rem;
  color: var(--earth);
  max-width: 600px;
  margin: 0 auto 2rem;
  line-height: 1.6;
}

.articles-filters {
  padding: 2rem 0 3rem;
  border-bottom: 1px solid var(--glass-border);
  margin-bottom: 3rem;
}

.filter-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  align-items: center;
}

.search-box {
  position: relative;
  max-width: 400px;
  width: 100%;
}

.search-input {
  width: 100%;
  padding: 1rem 3rem 1rem 1.5rem;
  border: 1px solid var(--glass-border);
  border-radius: var(--radius-full);
  background: white;
  font-size: 1rem;
  outline: none;
  transition: all var(--transition-base);
  box-shadow: var(--shadow-sm);
}

.search-input:focus {
  border-color: var(--accent);
  box-shadow: 0 5px 15px rgba(212, 165, 116, 0.2);
}

.search-icon {
  position: absolute;
  right: 1.5rem;
  top: 50%;
  transform: translateY(-50%);
  color: var(--earth);
  pointer-events: none;
}

.category-filters {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  justify-content: center;
}

.filter-btn {
  background: var(--glass);
  border: 1px solid var(--glass-border);
  color: var(--dark);
  padding: 0.8rem 1.5rem;
  border-radius: var(--radius-full);
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  cursor: pointer;
  transition: all var(--transition-base);
  backdrop-filter: blur(10px);
}

.filter-btn:hover,
.filter-btn.active {
  background: linear-gradient(135deg, var(--accent), var(--terracotta));
  color: white;
  border-color: var(--accent);
  transform: translateY(-2px);
}

.articles-stats {
  text-align: center;
  margin-bottom: 2rem;
  color: var(--earth);
  font-weight: var(--font-weight-medium);
}

.no-articles,
.no-results {
  padding: 4rem 0;
}

.empty-state {
  text-align: center;
  max-width: 400px;
  margin: 0 auto;
}

.empty-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
  opacity: 0.6;
}

.empty-state h3 {
  font-family: var(--font-display);
  font-size: 1.8rem;
  color: var(--dark);
  margin-bottom: 1rem;
}

.empty-state p {
  color: var(--earth);
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.load-more-container {
  text-align: center;
  padding: 3rem 0;
}

.load-more-btn {
  position: relative;
}

.load-more-btn.loading::after {
  content: '';
  position: absolute;
  right: 1rem;
  top: 50%;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  border: 2px solid transparent;
  border-top: 2px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: translateY(-50%) rotate(0deg); }
  100% { transform: translateY(-50%) rotate(360deg); }
}

/* Animation d'entrée des cartes */
.article-card.fade-in {
  animation-delay: var(--delay, 0s);
}

/* Responsive */
@media (max-width: 768px) {
  .articles-page {
    padding-top: 4rem;
  }
  
  .articles-hero {
    padding: 2rem 0 1rem;
  }
  
  .page-title {
    font-size: 2.5rem;
  }
  
  .page-subtitle {
    font-size: 1rem;
  }
  
  .filter-container {
    gap: 1.5rem;
  }
  
  .category-filters {
    gap: 0.3rem;
  }
  
  .filter-btn {
    padding: 0.6rem 1rem;
    font-size: 0.8rem;
  }
  
  .search-box {
    max-width: 100%;
  }
}

@media (max-width: 480px) {
  .category-filters {
    flex-direction: column;
    align-items: center;
    width: 100%;
  }
  
  .filter-btn {
    width: 100%;
    max-width: 250px;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const searchInput = document.getElementById('search-articles');
  const filterBtns = document.querySelectorAll('.filter-btn');
  const articlesContainer = document.getElementById('articles-container');
  const noResults = document.getElementById('no-results');
  const allArticles = document.querySelectorAll('.article-card');
  
  let currentFilter = 'all';
  let currentSearch = '';
  
  // Fonction de filtrage
  function filterArticles() {
    let visibleCount = 0;
    
    allArticles.forEach((article, index) => {
      const category = article.dataset.category;
      const title = article.dataset.title;
      const content = article.dataset.content;
      
      const matchesFilter = currentFilter === 'all' || category === currentFilter;
      const matchesSearch = currentSearch === '' || 
                           title.includes(currentSearch) || 
                           content.includes(currentSearch);
      
      if (matchesFilter && matchesSearch) {
        article.style.display = 'block';
        // Animation d'apparition décalée
        article.style.setProperty('--delay', (visibleCount * 0.1) + 's');
        article.classList.remove('fade-in');
        setTimeout(() => article.classList.add('fade-in'), 50);
        visibleCount++;
      } else {
        article.style.display = 'none';
      }
    });
    
    // Afficher/masquer le message "aucun résultat"
    if (visibleCount === 0) {
      noResults.style.display = 'block';
      articlesContainer.style.display = 'none';
    } else {
      noResults.style.display = 'none';
      articlesContainer.style.display = 'grid';
    }
  }
  
  // Gestion des filtres par catégorie
  filterBtns.forEach(btn => {
    btn.addEventListener('click', () => {
      filterBtns.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      currentFilter = btn.dataset.filter;
      filterArticles();
    });
  });
  
  // Gestion de la recherche
  if (searchInput) {
    searchInput.addEventListener('input', (e) => {
      currentSearch = e.target.value.toLowerCase();
      filterArticles();
    });
  }
  
  // Fonction de réinitialisation
  window.resetFilters = function() {
    currentFilter = 'all';
    currentSearch = '';
    if (searchInput) searchInput.value = '';
    filterBtns.forEach(b => b.classList.remove('active'));
    filterBtns[0].classList.add('active');
    filterArticles();
  };
  
  // Animation d'entrée initiale
  allArticles.forEach((article, index) => {
    article.style.setProperty('--delay', (index * 0.1) + 's');
  });
});
</script>