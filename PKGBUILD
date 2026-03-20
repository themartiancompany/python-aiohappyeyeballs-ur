#} SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.


# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Daniel M. Capella
#     <polyzen@archlinux.org>
# Contributors:
#   Łukasz Tuz
#     <lukasz.tuz@gmail.com>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  # _git="${_evmfs}"
  _git="false"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_git_http" ]]; then
  _git_http="${_git_service}"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_py="python"
_pyver="$(
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$((
  ${_pyminver} + 1))"
_pkg=aiohappyeyeballs
_name="${_pkg}"
pkgbase="${_py}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=2.3.4
_commit="c8fecf6d70dcd5ccc2d11b3e269dacea69f77052"
pkgrel=4
_pkgdesc=(
  'Happy Eyeballs for asyncio.'
)
pkgdesc="${_pkg[*]}"
arch=(
  "any"
)
_http="https://${_git_http}.com"
if [[ ! -v "_ns" ]]; then
  _ns="aio-libs"
fi
url="${_http}/${_ns}/${_pkg}"
license=(
  "PSF-2.0"
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-poetry-core"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-asyncio"
)
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_sum="SKIP"
_sig_sum="SKIP"
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum="b22996259fa3d6d2ff74b6084ac10a8bff0c3ae90c3c60bb89b654496d495746"
_github_sig_sum="abbca38f3eacdf37fb297e8e5a2f4dec85f0abba7b644c4d5336e58e258775bc"
if [[ "${_git_service}" == "github" ]]; then
  _sum="${_github_sum}"
  _sig_sum="${_github_sig_sum}"
  # Truocolo
  _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
elif [[ "${_git_service}" == "gitlab" ]]; then
  _sum="${_gitlab_sum}"
  _sig_sum="${_gitlab_sig_sum}"
fi
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    _src=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
        _sum="${_gitlab_sum}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

build() {
  ls \
    -lsh
  cd \
    "${_pkg}-${_tag}"
  "${_py}" \
    -m \
      build \
      --wheel \
      --no-isolation
}

check() {
  cd \
    "${_pkg}-${_commit}"
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
    "${_pkg}-${_tag}"
  ls \
    -lsh
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
  # Symlink license file
  install \
    -vdm755 \
      "${pkgdir}/usr/share/licenses/${pkgname}/"
  ln \
    -s \
    "${_site_packages}/${_pkg}-${pkgver}.dist-info/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: ft=sh syn=sh et
