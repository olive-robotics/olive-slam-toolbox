# Olive SLAM Toolbox source release

This source distribution accompanies the slam_toolbox libraries in Olive's ARM64
Robot firmware. Olive adds source-delivery documentation, complete upstream
snapshots and license copies. No upstream implementation file is modified.

## Versions and correspondence

| ROS distribution | Package version | Official upstream commit | Matching installed files | Matching binary log locations |
| --- | --- | --- | --- | --- |
| Humble | 2.6.10 | `51a99767b3e2ed4076ae5763ff14b69343ffd884` | 47 | 96 |
| Jazzy | 2.8.5 | `02afdde003313a10b8d21461a92d9e5f4f0bc5f2` | 48 | 105 |

The package version did not change when upstream added the fixes in these
commits. Therefore the numbered tags `2.6.10` and `2.8.5` alone are insufficient
for the shipped libraries. The pinned commits above match all compared installed
headers, package metadata, launch/configuration files and logging locations.

The main tree follows the Jazzy commit; both complete snapshots are in
`source-release/`. Original source, CMake build rules, service definitions,
Karto sources and upstream Git history are retained.

The owner reports that official sources were used without local source changes.
[SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) records the compared files, SHA256
fingerprints and source-location checks. These checks support the selected
source revisions; they are not a byte-identical rebuild of the shipped binaries.
The original build machine's compiler configuration was not recovered.

## License notices

SLAM Toolbox includes LGPL-2.1 code and Karto SDK code under LGPL-3.0-or-later.
See the unchanged upstream `LICENSE`, `lib/karto_sdk/LICENSE`, and individual
source headers. Copies of GPL and LGPL texts are additionally included in
`source-release/LICENSES/`.

## Extract and build

Choose the snapshot for the ROS distribution being used; do not mix Humble and
Jazzy snapshots. `source-release/SHA256SUMS` covers archives and license copies.
For example, for Humble:

```sh
cd source-release
sha256sum -c SHA256SUMS
mkdir -p /tmp/olive-nav-build/src
tar -xzf slam-toolbox-humble-2.6.10-51a9976.tar.gz -C /tmp/olive-nav-build/src
mv /tmp/olive-nav-build/src/slam_toolbox-51a99767b3e2ed4076ae5763ff14b69343ffd884 /tmp/olive-nav-build/src/slam_toolbox
cd /tmp/olive-nav-build
. /opt/ros/humble/setup.sh
rosdep install --from-paths src --ignore-src --rosdistro humble -r -y
colcon build --packages-select slam_toolbox --cmake-args -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF
```

For Jazzy, select its archive and source `/opt/ros/jazzy/setup.sh`, and pass
`--rosdistro jazzy` to rosdep. Use a matching target architecture and compatible
ROS dependencies. The original `package.xml` files list dependencies and the
original `CMakeLists.txt` files control compilation and installation. Dependencies
resolved today can differ from the original build environment. No new binary
build or runtime replacement was performed for this source release.

The source-delivery documentation is on main, tagged `olive-slam-toolbox-sources-20261124`.
The exact upstream commits listed above remain available through Git history
and the included source archives.
