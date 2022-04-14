#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

pkgname=html-validate
pkgver=6.1.4
pkgrel=1
pkgdesc="Offline HTML5 validator. Validates either a full document or a smaller (incomplete) template, e.g. from an AngularJS or Vue.js component."
arch=('any')
url="https://github.com/npm/nopt"
license=('custom:ISC')
depends=('nodejs')
makedepends=('npm')
source=("https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz")
noextract=($pkgname-$pkgver.tgz)
sha512sums=('35e5410bb0a5d8fcc62ae787390c6b69849ab343cd2e9fc619edf7c5dc99fb887364997c2747c089d867d8ca8ba56709806c2f06e836a8e46097261f5f071f69')
options=("!strip")

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
