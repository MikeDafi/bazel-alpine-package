# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=2.2.0
pkgrel=0
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch="all"
license="ASL-2.0"
url='https://bazel.io/'
depends="bash openjdk8 libarchive zip unzip"
# coreutils can be removed as a make dependency once expr in busybox is compatible with the BSD version, see following bug reports:
# Patch bazel: https://github.com/bazelbuild/bazel/issues/4055
# https://bugs.alpinelinux.org/issues/8121
makedepends="coreutils git linux-headers protobuf python2 python3"
options="!distcc !strip !check"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"


build() {
  export JAVA_HOME=/usr/lib/jvm/default-jvm
  EXTRA_BAZEL_ARGS=--host_javabase=@local_jdk//:jdk ./compile.sh
  scripts/generate_bash_completion.sh --bazel=output/bazel --output=output/bazel-complete.bash --prepend=scripts/bazel-complete-template.bash
  output/bazel shutdown
  echo startup --server_javabase=$JAVA_HOME >> scripts/packages/bazel.bazelrc
}

package() {
  install -Dm755 ${srcdir}/scripts/packages/bazel.sh ${pkgdir}/usr/bin/bazel
  install -Dm755 ${srcdir}/scripts/packages/bazel.bazelrc ${pkgdir}/etc/bazel.bazelrc
  install -Dm755 ${srcdir}/output/bazel ${pkgdir}/usr/bin/bazel-real
  install -Dm644 ${srcdir}/output/bazel-complete.bash ${pkgdir}/usr/share/bash-completion/completions/bazel
  install -Dm644 ${srcdir}/scripts/zsh_completion/_bazel ${pkgdir}/usr/share/zsh/site-functions/_bazel
}
# vim:set ts=2 sw=2 et:

sha512sums="67011c3a045c0fd74cdcb98eef1c3ead6902a3bd65a629fe49911f9dbb4c39508bd91eb63c1fae68284136ad4994afb42a01c7f10983614e432f8be22a1c566e  bazel-2.2.0-dist.zip
403b5f68f9bb035423b9532dc7c4b1d7459e2e853fbc3bed9a6bb9030b5a22796f6d2b4e8928f4427fb7517dfa12f15e016899036f3d1c5ef54ade172f7a3db4  bazel-2.2.0-dist.zip.sig"
