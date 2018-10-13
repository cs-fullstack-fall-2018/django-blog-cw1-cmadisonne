# django-blog-cw1

Add edit blog post support to the blog project.

def post_edit(request, pk):
    post = get_object_or_404(Post, pk=pk)
    if request.method == "GET":
        post = PostForm(request.GET)
        if post.is_valid():
            post = post.save(commit=False)
            post.author = request.user
            post.published_date = timezone.now()
            post.save()
            return redirect('post_detail', pk=post.pk)
    else:
        post = PostForm()
    return render(request, 'blog_app/post_edit.html', {'post': post})
