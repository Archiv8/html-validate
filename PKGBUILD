#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/html-validate/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/html-validate/discussions>

pkgname=html-validate
pkgver=7.3.3
pkgrel=1
pkgdesc="Offline HTML5 validator. Validates either a full document or a smaller (incomplete) template, e.g. from an AngularJS or Vue.js component."
arch=(
  "any"
)
url="https://github.com/npm/nopt"
license=(
  "custom:ISC"
)
depends=(
  "nodejs"
)
makedepends=(
  "npm"
)
source=(
  "https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz"
)
noextract=(
  "$pkgname-$pkgver.tgz"
)
sha512sums=(
  "9c00739811d46fe4db8aa2dbde08280bbb8437998a8194b06c1fcba46c976eb23e6a35419f263244cb1c2c5399198a70e6069c059b6a90ae95cc553b8db5ce6e"
)
options=(
  "!strip"
)

# [ToDo]: Add jq etc to build
package() {
  npm install -g --prefix "$pkgdir"/usr "$srcdir"/$pkgname-$pkgver.tgz

  # Non-deterministic race in npm gives 777 permissions to random directories.
  # See https://github.com/npm/npm/issues/9359 for details.
  chmod -R u=rwX,go=rX "$pkgdir"

  # npm installs package.json owned by build user
  # https://bugs.archlinux.org/task/63396
  chown -R root:root "$pkgdir"

  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s ../../../lib/node_modules/$pkgname/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
