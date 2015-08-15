# $Id: PKGBUILD 35437 2010-12-20 13:49:41Z angvp $
# Maintainer: Angel Velasquez <angvp@archlinux.org>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: Rubin Simons <rubin@xs4all.nl>

pkgname=eclipse-ve
pkgver=1.5.0
pkgrel=1
_reldate=201012021328
pkgdesc="Visual Editor framework for the Eclipse platform"
arch=('any')
url="http://www.eclipse.org/vep/"
license=('EPL')
depends=('eclipse-emf' 'eclipse-gef')

# Source doesn't exist
#source=(http://download.eclipse.org/tools/ve/downloads/drops/${pkgver}/R${_reldate}/VE-Update-${pkgver}.zip)
#md5sums=('49dba69a94960dcff11b239f89ca112d')
# Perhaps there's better luck with this one?
#source=("http://archive.eclipse.org/tools/archives/ve.tgz")

build() {
  _dest=${pkgdir}/usr/share/eclipse/dropins/${pkgname/eclipse-}/eclipse

  cd ${srcdir}

  # Features
  find features -type f | while read _feature ; do
    if [[ ${_feature} =~ (.*\.jar$) ]] ; then
      install -dm755 ${_dest}/${_feature%.jar}
      cd ${_dest}/${_feature/.jar}
      jar xf ${srcdir}/${_feature} || return 1
      cd - >/dev/null 2>&1
    else
      install -Dm644 ${_feature} ${_dest}/${_feature}
    fi
  done

  # Plugins
  find plugins -type f | while read _plugin ; do
    install -Dm644 ${_plugin} ${_dest}/${_plugin}
  done
  cd ${_dest}/plugins
  for _plugin in *.jar.pack.gz ; do
    gunzip -q ${_plugin}
    unpack200 -qr ${_plugin%.gz} ${_plugin%.pack.gz}
  done

  # Other
  install -Dm644 ${srcdir}/{artifacts,content}.jar ${_dest}
}

# vim:set ts=2 sw=2 et:
md5sums=('ecb54b171bb8583623bc184b7e340e97')
