
pkgdesc="ROS - These are lightweight text streaming classes that connect to standardised ecl type devices."
url='http://www.ros.org/'

pkgname='ros-hydro-ecl-streams'
pkgver='0.60.8'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-ecl-devices
  ros-hydro-ecl-concepts
  ros-hydro-ecl-license
  ros-hydro-ecl-type-traits
  ros-hydro-ecl-converters
  ros-hydro-ecl-errors
  ros-hydro-catkin
  ros-hydro-ecl-time)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-hydro-ecl-devices
  ros-hydro-ecl-concepts
  ros-hydro-ecl-license
  ros-hydro-ecl-type-traits
  ros-hydro-ecl-converters
  ros-hydro-ecl-errors
  ros-hydro-ecl-time)
depends=(${ros_depends[@]})

_tag=release/hydro/ecl_streams/${pkgver}-${_pkgver_patch}
_dir=ecl_streams
source=("${_dir}"::"git+https://github.com/yujinrobot-release/ecl_core-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
