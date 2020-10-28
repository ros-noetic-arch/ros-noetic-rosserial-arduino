pkgdesc="ROS - rosserial for Arduino/AVR platforms."
url='https://wiki.ros.org/rosserial_arduino'

pkgname='ros-noetic-rosserial-arduino'
pkgver='0.9.1'
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(
	ros-noetic-catkin
    ros-noetic-message-generation
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-rospy
    ros-noetic-rosserial-msgs
    ros-noetic-rosserial-client
    ros-noetic-message-runtime
    ros-noetic-rosserial-python
)

depends=(
    arduino-avr-core
	${ros_depends[@]}
)

_dir="rosserial-${pkgver}/rosserial_arduino"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-drivers/rosserial/archive/${pkgver}.tar.gz")
sha256sums=('0e4dbb4d6e456c354ee04f552cc36b43d053dc3f5a8bbfccff7f8adf3ae48534')

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
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
