# Testing: CI/CD (Continuous Integration)

Automating checks on GitHub or GitLab prevents buggy code from reaching production.

## GitHub Actions
Example workflow (`.github/workflows/php.yml`):
```yaml
name: PHP tests
on: [push, pull_request]
jobs:
  php-linter:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: prestashop/github-action-php-lint/7.3@master

  phpstan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: composer install
      - name: Run PHPStan
        run: docker run --rm -v $PWD:/web/module phpstan/phpstan analyse --configuration=/web/module/tests/phpstan/phpstan.neon
```

## Artifact Building
Automate the creation of the module zip file, ensuring `vendor/` is included but `node_modules/` and dev-dependencies are removed.
```bash
composer install --no-dev -o
zip -r mymodule.zip . -x "tests/*" ".git/*"
```
