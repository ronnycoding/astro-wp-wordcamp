README.md

2.03 KB • 57 extracted lines

Formatting may be inconsistent from source.
# Astro + WordPress Starter Kit

This project demonstrates how to use Astro with WordPress as a headless CMS, creating a fast, static site with dynamic content.

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   ├── layouts/
│   │   └── Layout.astro
│   └── pages/
│       ├── index.astro
│       └── [slug].astro
├── docker-compose.yml
└── package.json
```

- `src/pages/index.astro`: The main page that fetches and displays a list of posts from WordPress.
- `src/pages/[slug].astro`: A dynamic route for individual blog posts.
- `docker-compose.yml`: Configuration for running WordPress and MariaDB locally.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `docker-compose up -d`    | Start WordPress and MariaDB containers           |
| `docker-compose down`     | Stop and remove the containers                   |

## 🔧 Configuration

1. Start the WordPress environment:
   ```
   docker-compose up -d
   ```
2. Access WordPress at `http://localhost:8086` and set up your site.
3. Update the API endpoint in `src/pages/index.astro` and `src/pages/[slug].astro` if necessary.

## 🚀 Building and Deploying

1. Run `npm run build` to generate your static site.
2. Deploy the contents of the `dist/` directory to your hosting provider.

## 👀 Want to learn more?

- [Astro Documentation](https://docs.astro.build)
- [WPGraphql](https://www.wpgraphql.com/)

## Plugin Management

To install and activate a plugin:

```bash
docker exec wpcli wp plugin install [plugin-slug|zip-url] --activate
```

Replace `[plugin-slug|zip-url]` with either the plugin's slug from the WordPress repository or a direct URL to the plugin's zip file.

## Theme Creation

To create a new WordPress theme:

```bash
docker exec wpcli wp scaffold _s sample-theme --theme_name="Sample Theme" --author="John Doe"
```

This command creates a new theme based on the `_s` (Underscores) starter theme. Customize the `sample-theme`, `"Sample Theme"`, and `"John Doe"` parameters as needed.

## Installing Essential Plugins

Here's a list of recommended plugins along with their installation commands:

```bash
# GraphQL API for WordPress
docker exec wpcli wp plugin install wp-graphql --activate

# Headless Mode
docker exec wpcli wp plugin install headless-mode --activate

# Yoast SEO
docker exec wpcli wp plugin install wordpress-seo --activate

# Add WPGraphQL SEO
docker exec wpcli wp plugin install add-wpgraphql-seo --activate

# WPGraphQL Gutenberg
docker exec wpcli wp plugin install https://github.com/pristas-peter/wp-graphql-gutenberg/archive/refs/heads/develop.zip --activate

# WPGraphQL Content Blocks
docker exec wpcli wp plugin install https://github.com/wpengine/wp-graphql-content-blocks/releases/latest/download/wp-graphql-content-blocks.zip --activate

# Advanced Custom Fields Pro
docker exec wpcli wp plugin install https://github.com/wordpress-premium/advanced-custom-fields-pro/archive/refs/heads/master.zip  --activate

# WPGraphQL for ACF
docker exec wpcli wp plugin install wpgraphql-acf --activate

# Contact Form 7
docker exec wpcli wp plugin install contact-form-7 --activate

# JWT Authentication for WP REST API
docker exec wpcli wp plugin install jwt-authentication-for-wp-rest-api --activate

# Add CORS support
docker exec wpcli wp plugin install wp-cors --activate

# Total Counts for WPGraphQL (Nice to paginate queries)
docker exec wpcli wp plugin install git@github.com:builtbycactus/total-counts-for-wp-graphql.git --activate
```

## Custom ACF Block Registration

Instead of creating custom Gutenberg blocks, we'll use ACF to register blocks. Create a plugin named `register-acf-blocks` with the following structure:

```php
<?php
/**
 * Plugin Name: register-acf-blocks
 * Plugin URI: https://yourwebsite.com/
 * Description: This plugin is to register ACF blocks.
 * Version: 0.1
 * Author: Your Name
 * Author URI: https://yourwebsite.com/
 **/

add_action("acf/init", "register_acf_blocks_init");
function register_acf_blocks_init() {
    if (function_exists("acf_register_block")) {
        // Register your blocks here
        acf_register_block([
            "name" => "example-block",
            "title" => __("Example Block"),
            "description" => __("A custom example block."),
            "render_callback" => "render_example_block",
            "category" => "theme",
            "icon" => "admin-comments",
        ]);
    }
}

function render_example_block($block) {
    // Render your block content here
}
```

Activate the plugin:

```bash
docker exec wpcli wp plugin activate register-acf-blocks
```
