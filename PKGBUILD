# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://aur.archlinux.org/packages/mkinitcpio-nosystemd/
# 						Maintainer: Dave Reisner <dreisner@archlinux.org>
# 						Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=23
pkgrel=2
pkgdesc="Modular initramfs image creation utility"
arch=('any')
url="https://projects.archlinux.org/mkinitcpio.git/"
license=('GPL')
depends=('awk' 'mkinitcpio-busybox>=1.19.4-2' 'kmod' 'util-linux>=2.23' 'libarchive'
         'coreutils' 'bash' 'findutils' 'grep' 'filesystem>=2011.10-1' 'gzip' 'lz4')
optdepends=('xz: Use lzma or xz compression for the initramfs image'
            'bzip2: Use bzip2 compression for the initramfs image'
            'lzop: Use lzo compression for the initramfs image'
            'mkinitcpio-nfs-utils: Support for root filesystem on NFS')
makedepends=('asciidoc')
provides=("mkinitcpio=${pkgver}-${pkgrel}")
backup=('etc/mkinitcpio.conf')
source=("https://sources.archlinux.org/other/${pkgname}/${pkgname}-$pkgver.tar.gz"
 		'0002-remove-systemd.patch')
install=mkinitcpio.install
sha256sums=('913cd9f5629dff6c59e46ed9d44d5af8d4a0d2bddba0a1faffe716dc28bcf152'
            '4921518d130b73724645b3732ba471005b8755a89a219bb6396e3b082414bb78')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  #start removing systemd related stuff
  local d=${srcdir}/${pkgname}-${pkgver}
  [ ! -h "$d" ] && ln -s ${pkgname}-${pkgver} "$d"
  [ ! -d "$d" ] && echo "!!!!! cannot locate dir '$d'" && exit 666
  rm -rf ${d}/install/sd-vconsole ${d}/install/sd-shutdown ${d}/systemd ${d}/tmpfiles
  patch -d "$pkgname-$pkgver" -Np1 <0002-remove-systemd.patch
}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "${pkgname}-$pkgver" DESTDIR="$pkgdir" install
}
