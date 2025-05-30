# 首页

<div class="home-blog-title">
书记
</div>


<div class="home-blog-title">
日志
</div>

<div class="home-blog-list" class="home-blog-list"></div>

<style>
    .home-blog-title {
        font-size:22px;
        margin: 1rem 0;
        padding: 1rem 0 0 1rem;
        border-top: 1px solid blue;
    }
</style>

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