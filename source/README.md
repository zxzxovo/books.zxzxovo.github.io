# 首页

<div class="text-xl px-4 py-2 mb-4 border-b border-gray-400 dark:border-gray-600">
#书 籍
</div>

<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4 p-4">
  <a href="./books/tokio-docs/index.html" target="_blank" 
     class="block bg-white dark:bg-gray-800 rounded-lg shadow-md hover:shadow-lg dark:shadow-gray-700 transition-all duration-300 border border-gray-200 dark:border-gray-600 hover:border-gray-300 dark:hover:border-gray-500 overflow-hidden hover:-translate-y-0.5">
    <div class="p-4">
      <h3 class="text-base font-semibold text-gray-800 dark:text-gray-200 mb-2 text-center">
        Tokio中文文档
      </h3>
      <p class="text-xs text-gray-600 dark:text-gray-400 text-center leading-relaxed">
        Tokio文档的中文翻译
      </p>
    </div>
  </a>
</div>

<div class="text-xl px-4 py-2 mb-4 border-b border-gray-400 dark:border-gray-600">
#日 志
</div>

<div id="home-blog-list" class="px-4"></div>

<script>
    // load blogs
    documentReady(async ()=>{
        const resp = await fetch('/blogs/all/index.json');
        let blogs = await resp.json();
        if (blogs.length > 20) {
            blogs = blogs.slice(0, 20);
        }
        console.log(JSON.stringify(blogs));
        const items = blogs.map(blog => {
            let date = new Date(blog.date).toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });
            return `
<div class="home-blog-list-item">
    <div><span class="text-sm font-semibold uppercase">${date}</span></div>
    <div><a href="${blog.uri}">${gitsite.encodeHtml(blog.title)}</a></div>
</div>`;
        });
        document.getElementById('home-blog-list').innerHTML = items.join('');
    });
</script>

