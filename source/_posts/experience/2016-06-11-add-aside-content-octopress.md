---
layout: post
title: "[Octopress] Add Aside Content to Octopress "
comments: true
category: experience

---

# Aside

Example of this is the 'categories' list on the right hand side of the blog page. It's always pinned on RHS regardless of page content.

# Instruction

1. Add to source/_includes/asides/category_list.html with the following content. (remember to delete [delete-this-tag])

        <section class="well">
          <h1>Categories</h1>
          <ul id="categories" class="nav nav-list">
            {[delete-this-tag]% category_list %[delete-this-tag]}
          </ul>
        </section>

1. Go to _config.yml and modify default_asides.

        default_asides: [asides/category_list.html, asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html, asides/advertise.html]

1. Since the 'category_list' tag is not natively supported. Add plugins/category_list_tag.rb with the [followin content](https://kaworu.ch/blog/2013/09/23/categories-page-with-octopress/).

        module Jekyll
          class CategoryListTag < Liquid::Tag
            def render(context)
              html = ""
              categories = context.registers[:site].categories.keys
              categories.sort.each do |category|
                posts_in_category = context.registers[:site].categories[category].size
                category_dir = context.registers[:site].config['category_dir']
                category_url = File.join(category_dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase)
                html << "<li class='category'><a href='/#{category_url}/'>#{category} (#{posts_in_category})</a></li>\n"
              end
              html
            end
          end
        end

        Liquid::Template.register_tag('category_list', Jekyll::CategoryListTag)

<<<<<<< HEAD
1. rake generate && rake preview
=======
1. rake generate && rake preview
>>>>>>> 0c97438afe650fd549605cc20093d02b773ee985
