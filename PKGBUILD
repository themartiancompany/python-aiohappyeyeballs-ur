# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Łukasz Tuz <lukasz.tuz@gmail.com>

pkgname=python-aiohappyeyeballs
_name=${pkgname#python-}
pkgver=2.3.4
pkgrel=1
pkgdesc='Happy Eyeballs for asyncio'
arch=(any)
url=https://github.com/aio-libs/aiohappyeyeballs
license=(PSF-2.0)
depends=(python)
makedepends=(
  git
  python-build
  python-installer
  python-poetry-core
)
checkdepends=(
  python-pytest
  python-pytest-asyncio
)
source=("git+$url.git#tag=v$pkgver")
b2sums=('a91db715db83854fd79edd793cbee20bf389d0f1f7ac46550b8f6b9cdb4cec56c0d5e8031f8624ff58f6498935bd87899c499c656c02537ea0c79722ec8180d9')

build() {
  cd "$_name"
  python -m build --wheel --no-isolation
}

check() {
  cd "$_name"
  # Override addopts as they invoke coverage testing
  pytest --override-ini="addopts=-v -Wdefault"
}

package() {
  cd "$_name"
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/"$_name"-$pkgver.dist-info/LICENSE \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
