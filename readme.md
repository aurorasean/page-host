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

## products.txt

The root landing page reads [`products.txt`](products.txt) at runtime to build the list of cards. Each non-blank, non-comment line must follow the format:

```
env/product
```

Example:

```
# staging builds
staging/product1
staging/product2

# production builds
prod/product1
prod/product2
```

- Lines starting with `#` are treated as comments and ignored.
- The order of lines controls the display order.
- `staging` and `prod` receive coloured badges automatically; any other environment name gets a neutral blue badge.

## Adding a New Product

1. Add a line to `products.txt`:
   ```
   staging/my-new-product
   prod/my-new-product
   ```
2. Create the corresponding directories and HTML files:
   ```bash
   mkdir -p staging/my-new-product prod/my-new-product
   # drop an index.html into each
   ```
3. Commit and push – the [deploy workflow](.github/workflows/deploy.yml) will publish the site automatically.

## Adding a New Environment

1. Add lines to `products.txt` using the new environment name, e.g.:
   ```
   preview/my-product
   ```
2. Create the directory and HTML files:
   ```bash
   mkdir -p preview/my-product
   ```
3. Commit and push.

## Deployment

The site is deployed automatically to **GitHub Pages** on every push to `main` via [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).

To enable GitHub Pages:
1. Go to **Settings → Pages** in this repository.
2. Set the source to **GitHub Actions**.
