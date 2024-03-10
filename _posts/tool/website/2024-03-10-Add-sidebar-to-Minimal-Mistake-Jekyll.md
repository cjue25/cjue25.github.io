---
title:  "Add Sidebar"
categories:
  - website
---

Refer to https://kcore.org/ source code.

*This is a note long after I finished the modification.
 the steps are not sure if all are included.*
 

### Step 1. Add `sidebar` and `nav` in `_config.yml`

```yml
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      show_date: true
      comments: true
      related: true
      classes: wide
      sidebar:
        nav: "site_sidebar"
```

### Step 2. Add `_includes/category-sidebar.html`

copy from [here](https://github.com/jdeluyck/kcoreorg-website/blob/master/_includes/category-sidebar.html)

### Step 3. Add following in `_includes/nav_list`

{`%` if nav.type == "categories" `%`}{`%` include_cached category-sidebar.html `%`}{`%` endif`%`}

### Step 4. Add `sidebar` in `_pages/posts.md`

```yml
sidebar:
  nav: "site_sidebar"
```

### Step 5. Add `categories` in wanted posts

```yml
categories:
  - anywords
```

### Step 6. Append `site_sidebar` in `_data/navigation.yml`

```yml
site_sidebar:
  - title: "Categories"
    type: categories
```