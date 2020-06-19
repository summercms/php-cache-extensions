<h1 align="center">Cache PHP extensions in GitHub Actions</h1>

<p align="center">
  <a href="https://github.com/shivammathur/cache-extensions" title="Cache PHP extensions in GitHub Actions"><img alt="GitHub Actions status" src="https://github.com/shivammathur/cache-extensions/workflows/Main%20workflow/badge.svg"></a>
  <a href="https://codecov.io/gh/shivammathur/cache-extensions" title="Code coverage"><img alt="Codecov Code Coverage" src="https://codecov.io/gh/shivammathur/cache-extensions/branch/master/graph/badge.svg"></a>
  <a href="https://github.com/shivammathur/cache-extensions/blob/master/LICENSE" title="license"><img alt="LICENSE" src="https://img.shields.io/badge/license-MIT-428f7e.svg"></a>
  <a href="#tada-php-support" title="PHP Versions Supported"><img alt="PHP Versions Supported" src="https://img.shields.io/badge/php-%3E%3D%205.3-8892BF.svg"></a>
</p>

Cache PHP extensions in [GitHub Actions](https://github.com/features/actions "GitHub Actions"). This action has to be used along with [shivammathur/setup-php](https://github.com/shivammathur/setup-php "Setup PHP") and [actions/cache](https://github.com/actions/cache "Cache in GitHub Actions") GitHub Actions. It configures the environment required to cache PHP extensions. Refer to [Usage](#memo-usage "How to use this") section to see how to use this.

## Contents

- [PHP Support](#tada-php-support)
- [OS/Platform Support](#cloud-osplatform-support)
- [Usage](#memo-usage)
  - [Inputs](#inputs)
  - [Workflow](#workflow)
- [License](#scroll-license)
- [Contributions](#1-contributions)
- [Support this project](#sparkling_heart-support-this-project)
- [Dependencies](#bookmark-dependencies)

## :tada: PHP Support

|PHP Version|Stability|Release Support|
|--- |--- |--- |
|5.3|`Stable`|`End of life`|
|5.4|`Stable`|`End of life`|
|5.5|`Stable`|`End of life`|
|5.6|`Stable`|`End of life`|
|7.0|`Stable`|`End of life`|
|7.1|`Stable`|`End of life`|
|7.2|`Stable`|`Security fixes only`|
|7.3|`Stable`|`Active`|
|7.4|`Stable`|`Active`|
|8.0|`Nightly`|`In development`|

## :cloud: OS/Platform Support

|Virtual environment|YAML workflow label|
|--- |--- |
|Windows Server 2019|`windows-latest` or `windows-2019`|
|Ubuntu 20.04|`ubuntu-20.04`|
|Ubuntu 18.04|`ubuntu-latest` or `ubuntu-18.04`|
|Ubuntu 16.04|`ubuntu-16.04`|
|macOS Catalina 10.15|`macos-latest` or `macOS-10.15`|

## :memo: Usage

### Inputs

#### `php-version` (required)

- Specify the PHP version you want to setup.
- Accepts a `string`. For example `'7.4'`.
- See [PHP support](#tada-php-support) for supported PHP versions.

#### `extensions` (required)

- Specify the extensions you want to add or remove.
- Accepts a `string` in csv-format. For example `mbstring, , xdebug, :opcache`.
- Extensions prefixed with `:` are ignored.

#### `key` (required)

- Specify the key to identify the cache version.
- Accepts any `string`. For example `cache-v1`.
- Changing this would reset the cache.

See [action.yml](action.yml "Metadata for this GitHub Action") and usage below for more info.

### Workflow
> Cache extensions in a PHP workflow

```yaml
jobs:
  run:
    runs-on: ${{ matrix.operating-system }}
    strategy:
      matrix:
        operating-system: [ubuntu-latest, windows-latest, macos-latest]
        php-versions: ['7.2', '7.3', '7.4']
    name: PHP ${{ matrix.php-versions }} Test on ${{ matrix.operating-system }}
    env:
      extensions: intl, pcov
      key: cache-v1 # can be any string, change to clear the extension cache.
    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Setup cache environment
      id: extcache
      uses: shivammathur/cache-extensions@v1
      with:
        php-version: ${{ matrix.php-versions }}
        extensions: ${{ env.extensions }}
        key: ${{ env.key }}

    - name: Cache extensions
      uses: actions/cache@v2
      with:
        path: ${{ steps.extcache.outputs.dir }}
        key: ${{ steps.extcache.outputs.key }}
        restore-keys: ${{ steps.extcache.outputs.key }}

    - name: Setup PHP
      uses: shivammathur/setup-php@v2
      with:
        php-version: ${{ matrix.php-versions }}
        extensions: ${{ env.extensions }}
```

## :scroll: License

The scripts and documentation in this project are released under the [MIT License](LICENSE "License for shivammathur/cache-extensions"). This project has multiple [dependencies](https://github.com/shivammathur/cache-extensions/network/dependencies "Dependencies for this PHP Action"). Their licenses can be found in their respective repositories.

## :+1: Contributions

Contributions are welcome! See [Contributor's Guide](.github/CONTRIBUTING.md "shivammathur/cache-extensions contribution guide"). If you face any issues while using this or want to suggest a feature/improvement, create an issue [here](https://github.com/shivammathur/cache-extensions/issues "Issues reported").

## :sparkling_heart: Support this project

If this action helped you.

- Sponsor the project by subscribing on [Patreon](https://www.patreon.com/shivammathur "Shivam Mathur Patreon") or by contributing using [Paypal](https://www.paypal.me/shivammathur "Shivam Mathur PayPal").
- Please star the project and share it with the community.
- If you blog, write about your experience of using this action.
- If you need any help using this, please contact me using [Codementor](https://www.codementor.io/shivammathur "Shivam Mathur Codementor")u need any help using this, please contact me using [Codementor](https://www.codementor.io/shivammathur "Shivam Mathur Codementor")

## :bookmark: Dependencies

- [Node.js dependencies](https://github.com/shivammathur/setup-php/network/dependencies "Node.js dependencies")