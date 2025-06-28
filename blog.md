---
layout: page
title: Blog
permalink: /blog/
---

<div class="posts">
  {% for post in site.posts %}
  <div class="post-card">
    <a href="{{ post.url | absolute_url }}">
      <div class="post-card-content">
        <h2 class="post-title">{{ post.title }}</h2>
        <span class="post-date">{{ post.date | date_to_string }}</span>
        {% if post.excerpt %}
          <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
      {% if post.categories.size > 0 %}
        <span class="post-categories">
          {% for category in post.categories %}
            <span class="category-tag">{{ category }}</span>{% unless forloop.last %}{% endunless %}
          {% endfor %}
        </span>
      {% endif %}
  </a>
</div>
{% endfor %}
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    console.log('DOM fully loaded and parsed.');
    const postsContainer = document.querySelector('.posts');
    if (!postsContainer) {
      console.error('Posts container not found!');
      return;
    }
    const posts = Array.from(postsContainer.querySelectorAll('.post-card'));
    console.log(`Found ${posts.length} post cards.`);

    // Create filter and sort controls
    const controlsDiv = document.createElement('div');
    controlsDiv.classList.add('blog-controls');

    // Category Filter
    const categoryLabel = document.createElement('label');
    categoryLabel.textContent = 'Filter by Category: ';
    const categorySelect = document.createElement('select');
    categorySelect.id = 'category-filter';
    categorySelect.innerHTML = '<option value="all">All Categories</option>';

    // Get unique categories from posts
    const allCategories = new Set();
    posts.forEach(post => {
      const categoriesSpan = post.querySelector('.post-categories');
      if (categoriesSpan) {
        // Extract categories from the new tag structure
        const categoryTags = categoriesSpan.querySelectorAll('.category-tag');
        if (categoryTags.length > 0) {
           categoryTags.forEach(tag => allCategories.add(tag.textContent.trim()));
        }
      }
    });

    allCategories.forEach(category => {
      const option = document.createElement('option');
      option.value = category;
      option.textContent = category;
      categorySelect.appendChild(option);
    });
    console.log('Unique categories found:', Array.from(allCategories));


    controlsDiv.appendChild(categoryLabel);
    controlsDiv.appendChild(categorySelect);

    // Sort Select
    const sortLabel = document.createElement('label');
    sortLabel.textContent = 'Sort by: ';
    const sortSelect = document.createElement('select');
    sortSelect.id = 'sort-select';
    sortSelect.innerHTML = `
      <option value="date">Date</option>
      <option value="title">Title</option>
    `;

    controlsDiv.appendChild(sortLabel);
    controlsDiv.appendChild(sortSelect);

    // Insert controls before posts
    postsContainer.parentNode.insertBefore(controlsDiv, postsContainer);
    console.log('Filter and sort controls added.');

    // Function to filter and sort posts
    function filterAndSortPosts() {
      console.log('Filtering and sorting posts...');
      const selectedCategory = categorySelect.value;
      const sortBy = sortSelect.value;
      console.log(`Selected Category: ${selectedCategory}, Sort By: ${sortBy}`);


      posts.forEach(post => {
        const categoriesSpan = post.querySelector('.post-categories');
        // Extract categories from the new tag structure for filtering
        const categories = categoriesSpan ? Array.from(categoriesSpan.querySelectorAll('.category-tag')).map(tag => tag.textContent.trim()) : [];
        const matchesCategory = selectedCategory === 'all' || categories.includes(selectedCategory);

        if (matchesCategory) {
          post.classList.remove('hidden'); // Show the post by removing the hidden class
        } else {
          post.classList.add('hidden'); // Hide the post by adding the hidden class
        }
      });
      console.log('Filtering complete.');


      // Sort visible posts
      const visiblePosts = posts.filter(post => !post.classList.contains('hidden'));
      console.log(`Visible posts after filtering: ${visiblePosts.length}`);


      visiblePosts.sort((a, b) => {
        if (sortBy === 'date') {
          const dateA = new Date(a.querySelector('.post-date').textContent);
          const dateB = new Date(b.querySelector('.post-date').textContent);
          return dateB - dateA; // Sort by date descending
        } else if (sortBy === 'title') {
          const titleA = a.querySelector('.post-title').textContent.toLowerCase();
          const titleB = b.querySelector('.post-title').textContent.toLowerCase();
          if (titleA < titleB) return -1;
          if (titleA > titleB) return 1;
          return 0; // Sort by title alphabetically
        }
        return 0;
      });
      console.log('Sorting complete.');


      // Reorder posts in the DOM
      // Reorder posts in the DOM by appending them in the new order
      visiblePosts.forEach(post => {
        postsContainer.appendChild(post);
      });
    }

    // Add event listeners
    categorySelect.addEventListener('change', filterAndSortPosts);
    sortSelect.addEventListener('change', filterAndSortPosts);
    console.log('Event listeners added.');


    // Initial display
    filterAndSortPosts();
    console.log('Initial filter and sort applied.');

  });
</script>
