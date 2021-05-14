# Maintainer: Nev Delap <nevdelap at gmail dot com>
pkgname="ned"
pkgver="1.2.9"
pkgrel=1
pkgdesc="Like grep but with a powerful replace, unlike sed, it's not only line oriented."
arch=("x86_64")
url="https://github.com/nevdelap/ned"
license=("GPL3")
makedepends=()
source=("$pkgname-$pkgver.tar.gz::https://github.com/nevdelap/ned/archive/release.$pkgver.tar.gz")
md5sums=('3fe2b86055f4b94e03f4104c2cba9d57')

build() {
	curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && \
	. ~/.cargo/env && \
	rustup target add x86_64-unknown-linux-musl && \
	cd "ned-release.$pkgver" && \
	cargo build --release --target x86_64-unknown-linux-musl --locked
}

check() {
	cd "ned-release.$pkgver" && \
	. ~/.cargo/env && \
	cargo test --release --target x86_64-unknown-linux-musl --locked && \
	cargo fmt && \
	cargo clippy
}

package() {
	install -Dm755 "ned-release.$pkgver/target/x86_64-unknown-linux-musl/release/ned" "$pkgdir/usr/bin/ned" && \
	gzip < "ned-release.$pkgver/man/ned.1" > "ned-release.$pkgver/man/ned.1.gz" && \
	install -Dm 0644 "ned-release.$pkgver/man/ned.1.gz" "$pkgdir/usr/share/man/man1/ned.1.gz"
}
