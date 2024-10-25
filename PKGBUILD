# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Łukasz Tuz <lukasz.tuz@gmail.com>

_py="python"
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_name=aiohappyeyeballs
pkgname="${_py}-${_name}"
pkgver=2.3.4
pkgrel=1
pkgdesc='Happy Eyeballs for asyncio'
arch=(
  any
)
_http="https://github.com"
_ns="aio-libs"
url="${_http}/${_ns}/${_name}"
license=(
  PSF-2.0
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  git
  "${_py}-build"
  "${_py}-installer"
  "${_py}-poetry-core"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-asyncio"
)
source=(
  "git+${url}.git#tag=v$pkgver"
)
b2sums=(
  'a91db715db83854fd79edd793cbee20bf389d0f1f7ac46550b8f6b9cdb4cec56c0d5e8031f8624ff58f6498935bd87899c499c656c02537ea0c79722ec8180d9'
)

build() {
  cd \
    "${_name}"
  "${_py}" \
    -m \
      build \
      --wheel \
      --no-isolation
}

check() {
  cd \
    "${_name}"
  # Override addopts as they invoke coverage testing
  pytest \
    --override-ini="addopts=-v -Wdefault"
}

package() {
  local \
    _site_packages \
    _site_packages_cmd=()
  _site_packages_cmd=(
    "import site;"
    "print("
      "site.getsitepackages()[0]"
    ")"
  )
  _site_packages=$( \
    "${_py}" \
      -c \
        "${_site_packages_cmd[*]}")
  cd \
    "${_name}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  # Symlink license file
  install \
    -d \
      "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_name}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: ft=sh syn=sh et
