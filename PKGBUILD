pkgdesc="ROS - Generalized client side source for rosserial."
url='https://wiki.ros.org/rosserial_client'

pkgname='ros-noetic-rosserial-client'
pkgver='0.9.2'
arch=('any')
pkgrel=3
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
    ros-noetic-rosbash
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-rosserial-msgs
    ros-noetic-std-msgs
    ros-noetic-rospy
    ros-noetic-tf
    ros-noetic-rosunit
)

depends=(
	${ros_depends[@]}
)

_dir="rosserial-${pkgver}/rosserial_client"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-drivers/rosserial/archive/${pkgver}.tar.gz"
        "${pkgname}-${pkgver}-c5e90cd.patch"::"https://github.com/ros-drivers/rosserial/commit/c5e90cdd34aafca9783addbd8e83364b0fef4579.patch")
sha256sums=('10544be94241499aa3b019aea6d7cb40546ea484749e909cee31a928c7d40465'
			'5e06236fe3cc787b27b0cae7250ca6d37764b72e3a08f88130d2f98ddf92626a')

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCMAKE_BUILD_TYPE=Release \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python3 \
		-DPYTHON_INCLUDE_DIR=/usr/include/python3.7m \
		-DPYTHON_LIBRARY=/usr/lib/libpython3.7m.so \
		-DPYTHON_BASENAME=.cpython-37m \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
