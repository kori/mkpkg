env:
  pkgver: 2.26
  pkgpatch: 0

package:
  name: glibc
  version: $pkgver.$pkgpatch
  description: Glibc
  license:
    - GPL
    - LGPL
  skip_check: true

  source:
    - http://ftp.gnu.org/gnu/$name/$name-$pkgver.tar.xz

  build:
    - |
      echo "slibdir=/usr/lib" >> configparms
      echo "rtlddir=/usr/lib" >> configparms
      echo "sbindir=/usr/bin" >> configparms
      echo "rootsbindir=/usr/bin" >> configparms
    - $name-$pkgver/configure
          --prefix=/usr
          --libdir=/usr/lib
          --libexecdir=/usr/lib
          --enable-add-ons
          --enable-bind-now
          --disable-profile
          --enable-stackguard-randomization
          --enable-stack-protector=strong
          --enable-lock-elision
          --enable-multi-arch
          --disable-werror

      # build libraries with fortify disabled
    - echo "build-programs=no" >> configparms
    - make

      # re-enable fortify for programs
    - sed -i "/build-programs=/s#no#yes#" configparms

    - |
      echo "CC += -D_FORTIFY_SOURCE=2" >> configparms
      echo "CXX += -D_FORTIFY_SOURCE=2" >> configparms
    - make

  install:
    - make install_root="$pkgdir" install
    - |
      for f in libdl.so.2 libm.so.6 librt.so.1; do
        strip --strip-unneeded "$pkgdir"/usr/lib/"$f"
      done
