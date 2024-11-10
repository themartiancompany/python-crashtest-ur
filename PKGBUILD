# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

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
_pkg=crashtest
pkgname="${_py}-${_pkg}"
pkgver=0.4.1
pkgrel=3
pkgdesc='supposedly makes exceptions handling and inspection easier'
arch=(
  any
)
_http="https://github.com"
_ns="sdipater"
url="${_http}/${_ns}/${_pkgname}"
license=(
  MIT
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-"{"build","installer","wheel"}
  "${_py}-poetry-core"
)
checkdepends=(
  "${_py}-pytest"
)
_archive="${_pkgname}-${pkgver}"
source=(
  "${url}/archive/${pkgver}/${_archive}.tar.gz"
)
sha256sums=(
  '4ff59d9bee6d2bc581d462888ec28beb30ad448042c885a2b4ab45dc4910780b'
)
b2sums=(
  'aa46efb2dbabfeaab54f9149da42cb033f5dca3ab1c75032ca2542018058cf16775f56450cadf3e1272e738d602f32f21b9a6668a99f2733cd53d23c1754a0bc'
)

build(){
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      build \
    -wn
}

check() {
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      pytest
}

package() {
  cd \
    "${_archive}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm0644 \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/" \
    LICENSE
}
