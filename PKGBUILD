# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://aur.archlinux.org/packages/mkinitcpio-nosystemd/
# 						Maintainer: Dave Reisner <dreisner@archlinux.org>
# 						Maintainer: Thomas Bächler <thomas@archlinux.org>

pkgname=mkinitcpio
pkgver=23
pkgrel=3
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
 		'0002-remove-systemd.patch'
 		'0001-make-ldd-parsing-compatible-with-upstream-glibc-chan.patch')
install=mkinitcpio.install
sha256sums=('80f12a07f0dceef81dfe87200f099bd2149e0990391dda6defebaa5697f8a35a'
            '4921518d130b73724645b3732ba471005b8755a89a219bb6396e3b082414bb78'
            'f534892af930abf8164eead271dc012e42a552362fbb459e55e04d4a68b52a66')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  
  cd "$pkgname-$pkgver"
  #start removing systemd related stuff
  rm -rf install/sd-vconsole install/sd-shutdown systemd tmpfiles
  patch -p1 -i ../0002-remove-systemd.patch

  patch -p1 -i ../0001-make-ldd-parsing-compatible-with-upstream-glibc-chan.patch

}

check() {
  make -C "$pkgname-$pkgver" check
}

package() {
  make -C "${pkgname}-$pkgver" DESTDIR="$pkgdir" install
}
