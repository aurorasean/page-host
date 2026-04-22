# Page Host

A GitHub Pages repository for hosting static HTML pages across **multiple environments** and **multiple products**.

## URL Structure

```
https://<org>.github.io/page-host/                      ← landing page
https://<org>.github.io/page-host/staging/<product>/    ← staging environment
https://<org>.github.io/page-host/prod/<product>/       ← production environment
```

### Examples

| URL | Description |
|-----|-------------|
| `/staging/product1/` | Product 1 in the staging environment |
| `/staging/product2/` | Product 2 in the staging environment |
| `/prod/product1/`    | Product 1 in the production environment |
| `/prod/product2/`    | Product 2 in the production environment |

## Directory Structure

```
page-host/
├── index.html                  ← landing page (lists all envs & products)
├── staging/
│   ├── product1/
│   │   └── index.html
│   └── product2/
│       └── index.html
└── prod/
    ├── product1/
    │   └── index.html
    └── product2/
        └── index.html
```

## Adding a New Product

1. Create the required directories:
   ```bash
   mkdir -p staging/<new-product> prod/<new-product>
   ```
2. Add an `index.html` (or any HTML files) inside each directory.
3. Add a link card for the new product to the root `index.html` landing page.
4. Commit and push – the [deploy workflow](.github/workflows/deploy.yml) will publish the site automatically.

## Adding a New Environment

1. Create a top-level directory for the environment (e.g. `preview/`).
2. Add product subdirectories and HTML files inside it.
3. Add a new section for the environment in the root `index.html`.
4. Commit and push.

## Deployment

The site is deployed automatically to **GitHub Pages** on every push to `main` via [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).

To enable GitHub Pages:
1. Go to **Settings → Pages** in this repository.
2. Set the source to **GitHub Actions**.
