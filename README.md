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
