# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://aur.archlinux.org/packages/mkinitcpio-nosystemd/
# 						Maintainer: Dave Reisner <dreisner@archlinux.org>
# 						Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=24
pkgrel=3
pkgdesc="Modular initramfs image creation utility"
arch=(x86_64)
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
 		'0002-remove-systemd.patch'
 		'0001-Restore-addition-of-modules-from-config-file.patch')
install=mkinitcpio.install
sha256sums=('ec0ecbc518c14ecacf5a8ece2f068fe86fcaf3aed09ee6b82737e773e5d7d02b'
            '4921518d130b73724645b3732ba471005b8755a89a219bb6396e3b082414bb78'
            '563bf9be83bc378ded0ecafef2954ffc6e4d2f8599fd3d4ff5523068b093114d')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  
  cd "$pkgname-$pkgver"
  #start removing systemd related stuff
  rm -rf install/sd-vconsole install/sd-shutdown systemd tmpfiles
  patch -p1 -i ../0002-remove-systemd.patch

  patch -Np1 <"$srcdir"/0001-Restore-addition-of-modules-from-config-file.patch
}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "${pkgname}-$pkgver" DESTDIR="$pkgdir" install
}
