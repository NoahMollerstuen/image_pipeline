^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package image_proc
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

5.0.0 (2024-01-24)
------------------
* Port image_proc test to ROS 2 (`#910 <https://github.com/ros-perception/image_pipeline/issues/910>`_)
* Removed cfg files related with ROS 1 parameters (`#911 <https://github.com/ros-perception/image_pipeline/issues/911>`_)
  Removed cfg files related with ROS 1 parameters
* image_proc: consistent image_transport (`#884 <https://github.com/ros-perception/image_pipeline/issues/884>`_)
  * consistent image_transport parameter for crop_decimate, crop_non_zero
  and debayer nodes
  * consistent remapping support for compressed/etc topics in all three
  nodes
  * add lazy subscription support to crop_non_zero
  Additional minor fixes:
  * put the getTopicQosProfile() for publisher right in front of publisher
  declaration for clarity
* resize/recify: consistent image_transport (`#883 <https://github.com/ros-perception/image_pipeline/issues/883>`_)
  * support image_transport parameter
  * proper renaming so compressed/etc topics work as expected
  Additional minor fixes:
  * rename interpolation -> interpolation\_ for consistency
  * move parameter declaration BEFORE we create a publisher (and possibly
  get a subscriber created in connect callback)
  * put the getTopicQosProfile() for publisher right in front of publisher
  declaration for clarity
* ROS 2: Merged resize.cpp: fix memory leak (`#874 <https://github.com/ros-perception/image_pipeline/issues/874>`_)
  Related with this PR in ROS 1
  https://github.com/ros-perception/image_pipeline/pull/489
* allow use as component or node (`#852 <https://github.com/ros-perception/image_pipeline/issues/852>`_)
  This addresses
  https://github.com/ros-perception/image_pipeline/issues/823:
  * depth_image_proc was never implemented properly this way
  * image_proc might have once worked this way, but it appears upstream
  has changed over time and it was no longer doing the job.
  * stereo_image_proc is actually implemented correctly - I just added a
  comment
  With this PR:
  ```
  $ ros2 pkg executables image_proc
  image_proc crop_decimate_node
  image_proc crop_non_zero_node
  image_proc debayer_node
  image_proc image_proc
  image_proc rectify_node
  image_proc resize_node
  ```
  ```
  $ ros2 pkg executables depth_image_proc
  depth_image_proc convert_metric_node
  depth_image_proc crop_foremost_node
  depth_image_proc disparity_node
  depth_image_proc point_cloud_xyz_node
  depth_image_proc point_cloud_xyz_radial_node
  depth_image_proc point_cloud_xyzi_node
  depth_image_proc point_cloud_xyzi_radial_node
  depth_image_proc point_cloud_xyzrgb_node
  depth_image_proc point_cloud_xyzrgb_radial_node
  depth_image_proc register_node
  ```
* add support for lazy subscribers (`#815 <https://github.com/ros-perception/image_pipeline/issues/815>`_)
  This implements `#780 <https://github.com/ros-perception/image_pipeline/issues/780>`_ for ROS 2 distributions after Iron, where we have:
  * Connect/disconnect callbacks, per https://github.com/ros2/rmw/issues/330 (this made it into Iron)
  * Updated APIs in https://github.com/ros-perception/image_common/pull/272 (this is only in Rolling currently)
* add myself as a maintainer (`#846 <https://github.com/ros-perception/image_pipeline/issues/846>`_)
* Use the same QoS profiles as publishers in image_proc
* fix to allow remapping resize and image topics
* Contributors: Alejandro Hernández Cordero, Joe Schornak, Michael Ferguson, Michal Wojcik

3.0.1 (2022-12-04)
------------------
* Replace deprecated headers
  Fixing compiler warnings.
* add NOLINT to keep cpplint happy about curly brace being on new line
* Add conversion from YUV422-YUY2
* Contributors: Jacob Perron, Kenji Brameld, Tillmann Falck

3.0.0 (2022-04-29)
------------------
* Cleanup of image_proc.
* Some small fixes noticed while reviewing.
* Remove unnecessary find_package
* Deal with uncrustify and cpplint
* LTTng instrument image_proc::RectifyNode and image_proc::ResizeNode
* bring over ros1 fix for missing roi resize
* Add maintainer (`#667 <https://github.com/ros-perception/image_pipeline/issues/667>`_)
* Fix build with later versions of OpenCV 3
* Refactor image_proc and stereo_image_proc launch files (`#583 <https://github.com/ros-perception/image_pipeline/issues/583>`_)
* Contributors: Chris Lalancette, Evan Flynn, Jacob Perron, Scott K Logan, Víctor Mayoral Vilches

2.2.1 (2020-08-27)
------------------
* make crop_decimate work (`#593 <https://github.com/ros-perception/image_pipeline/issues/593>`_)
* remove email blasts from steve macenski (`#596 <https://github.com/ros-perception/image_pipeline/issues/596>`_)
* Disable "Publish Color!" debug_info (`#577 <https://github.com/ros-perception/image_pipeline/issues/577>`_)
* [Foxy] Use ament_auto Macros (`#573 <https://github.com/ros-perception/image_pipeline/issues/573>`_)
* Contributors: Dereck Wonnacott, Joshua Whitley, Michael Ferguson, Steve Macenski

2.2.0 (2020-07-27)
------------------
* Replacing deprecated header includes with new HPP versions. (`#566 <https://github.com/ros-perception/image_pipeline/issues/566>`_)
* Opencv 3 compatibility (`#564 <https://github.com/ros-perception/image_pipeline/issues/564>`_)
  * Remove GTK from image_view.
  * Reinstate OpenCV 3 compatibility.
* Fix bad quotes in image_proc launch file (`#563 <https://github.com/ros-perception/image_pipeline/issues/563>`_)
  This fixes a flake8 error.
* Contributors: Chris Lalancette, Jacob Perron, Joshua Whitley

* Initial ROS2 commit.
* Contributors: Michael Carroll

1.12.23 (2018-05-10)
--------------------

1.12.22 (2017-12-08)
--------------------
* Merge pull request `#311 <https://github.com/ros-perception/image_pipeline/issues/311>`_ from knorth55/revert-299
  Revert "Fix image_resize nodelet (`#299 <https://github.com/ros-perception/image_pipeline/issues/299>`_)"
  This reverts commit 32e19697ebce47101b063c6a02b95dfa2c5dbc52.
* Contributors: Shingo Kitagawa, Tully Foote

1.12.21 (2017-11-05)
--------------------
* Fix image_resize nodelet (`#299 <https://github.com/ros-perception/image_pipeline/issues/299>`_)
  Update interpolation types
  Add arguments to enable disable each nodelet
  Add default arguments for image_resize and image_rect
  Use toCVShare instead of toCVCopy
  Include image_resize in image_proc
* Updated fix for traits change. (`#303 <https://github.com/ros-perception/image_pipeline/issues/303>`_)
* Fix C++11 compilation
  This fixes `#292 <https://github.com/ros-perception/image_pipeline/issues/292>`_ and `#291 <https://github.com/ros-perception/image_pipeline/issues/291>`_
* [image_proc][crop_decimate] support changing target image frame_id (`#276 <https://github.com/ros-perception/image_pipeline/issues/276>`_)
* Contributors: Furushchev, Mike Purvis, Vincent Rabaud, bikramak

1.12.20 (2017-04-30)
--------------------
* Add nodelet to resize image and camera_info (`#273 <https://github.com/ros-perception/image_pipeline/issues/273>`_)
  * Add nodelet to resize image and camera_info
  * Depends on nodelet_topic_tools
  * Use recursive_mutex for mutex guard for dynamic reconfiguring
* Fix nodelet name: crop_nonZero ->  crop_non_zero (`#269 <https://github.com/ros-perception/image_pipeline/issues/269>`_)
  Fix https://github.com/ros-perception/image_pipeline/issues/217
* Fix permission of executable files unexpectedly (`#260 <https://github.com/ros-perception/image_pipeline/issues/260>`_)
* address gcc6 build error
  With gcc6, compiling fails with `stdlib.h: No such file or directory`,
  as including '-isystem /usr/include' breaks with gcc6, cf.,
  https://gcc.gnu.org/bugzilla/show_bug.cgi?id=70129.
  This commit addresses this issue for this package in the same way
  it was addressed in various other ROS packages. A list of related
  commits and pull requests is at:
  https://github.com/ros/rosdistro/issues/12783
  Signed-off-by: Lukas Bulwahn <lukas.bulwahn@oss.bmw-carit.de>
* Contributors: Kentaro Wada, Lukas Bulwahn

1.12.19 (2016-07-24)
--------------------

1.12.18 (2016-07-12)
--------------------

1.12.17 (2016-07-11)
--------------------

1.12.16 (2016-03-19)
--------------------
* clean OpenCV dependency in package.xml
* issue `#180 <https://github.com/ros-perception/image_pipeline/issues/180>`_ Check if all distortion coefficients are zero.
  Test with:
  rostest --reuse-master --text image_proc test_rectify.xml
  Can also test interactively with vimjay image_rect.launch, which brings up an rqt gui and camera info distortion coefficients can be dynamically reconfigured.
* Add a feature to crop the largest valid (non zero) area
  Remove unnecessary headers
  change a filename to fit for the ROS convention
* Contributors: Kenta Yonekura, Lucas Walter, Vincent Rabaud

1.12.15 (2016-01-17)
--------------------
* simplify OpenCV3 conversion
* Contributors: Vincent Rabaud

1.12.14 (2015-07-22)
--------------------

1.12.13 (2015-04-06)
--------------------
* fix dependencies
* Contributors: Vincent Rabaud

1.12.12 (2014-12-31)
--------------------

1.12.11 (2014-10-26)
--------------------

1.12.10 (2014-09-28)
--------------------

1.12.9 (2014-09-21)
-------------------
* get code to compile with OpenCV3
  fixes `#96 <https://github.com/ros-perception/image_pipeline/issues/96>`_
* Contributors: Vincent Rabaud

1.12.8 (2014-08-19)
-------------------

1.12.6 (2014-07-27)
-------------------

1.12.4 (2014-04-28)
-------------------

1.12.3 (2014-04-12)
-------------------

1.12.2 (2014-04-08)
-------------------

1.12.1 (2014-04-06)
-------------------
* get proper opencv dependency
* Contributors: Vincent Rabaud

1.11.7 (2014-03-28)
-------------------

1.11.6 (2014-01-29 00:38:55 +0100)
----------------------------------
- fix bad OpenCV linkage (#53)
