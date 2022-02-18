# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Eric Cheng <ericcheng@hey.com>
# Contributor: Ethan Skinner <aur@etskinner.com>
# Contributor: Grégoire Seux <grego_aur@familleseux.net>
# Contributor: Dean Galvin <deangalvin3@gmail.com>
# Contributor: NicoHood <archlinux@nicohood.de>

pkgname=home-assistant
pkgdesc='Open source home automation that puts local control and privacy first'
pkgver=2022.2.8
pkgrel=1
arch=(any)
url=https://home-assistant.io/
license=(APACHE)
depends=(
  gcc
  python-aiohttp
  python-aiohttp-cors
  python-astral
  python-async-timeout
  python-atomicwrites
  python-attrs
  python-awesomeversion
  python-bcrypt
  python-certifi
  python-ciso8601
  python-cryptography
  python-defusedxml
  python-httpx
  python-jinja
  python-mutagen
  python-pillow
  python-pip
  python-pyjwt
  python-pytz
  python-requests
  python-ruamel-yaml
  python-slugify
  python-sqlalchemy
  python-voluptuous
  python-voluptuous-serialize
  python-yaml
  python-yarl
  python-zeroconf
)
makedepends=(
  git
  python-setuptools
)
optdepends=(
  'net-tools: Nmap host discovery'
  'openzwave: Z-Wave integration'
  'python-dtlssocket: Ikea Tradfri integration'
  'python-lxml: Meteo France integration'
)
_tag=e3a2b51f0345a4ae1decb9b3a2683e168b84b530
source=(
  git+https://github.com/home-assistant/home-assistant.git#tag=${_tag}
  home-assistant.service
)
b2sums=('SKIP'
        '4b099405b1ea0e5585e612e2bd9a0841ae0b4da7a66c28b44b934dc69af58baeea7f930792c37bf3167e889ee3d14470661b7fff016a80305b33d09fc31cf07d')

pkgver() {
  cd home-assistant
  git describe --tags
}

prepare() {
  cd home-assistant
  # lift hard dep constraints, we'll deal with breaking changes ourselves
  sed 's/==/>=/g' -i requirements.txt setup.cfg homeassistant/package_constraints.txt
  # allow pip >= 20.3 to be used
  sed 's/,<20.3//g' -i requirements.txt setup.cfg homeassistant/package_constraints.txt
  # remove python-yaml restriction
  sed 's/pyyaml>=6.0//g' -i requirements.txt setup.cfg homeassistant/package_constraints.txt
  sed 's/pyyaml==6.0//g' -i requirements.txt setup.cfg homeassistant/package_constraints.txt
}

build() {
  cd home-assistant
  python setup.py build
}

package() {
  cd home-assistant
  python setup.py install --root="${pkgdir}" --prefix=/usr --optimize=1 --skip-build
  install -Dm 644 ../home-assistant.service -t "${pkgdir}"/usr/lib/systemd/system/
}

# vim: ts=2 sw=2 et:
