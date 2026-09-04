# Kyon

Source: https://github.com/ADVRHumanoids/iit-kyon-ros-pkg

Source branch: `ibrido_ros2`

Source revision: `b9631ebf19c7230dfc7adb654422a11dd257ef77`

The four static descriptions are generated from `kyon_urdf/urdf/kyon.urdf.xacro`
and `kyon_srdf/srdf/kyon.srdf.xacro`. All variants use the legs and the source
model's default Varta battery, while cameras, lidar, Dagana grippers, payloads,
and the xacro floating joint are disabled. The free-flyer is added by the
Example Robot Data loader.

| Description | Upper body | Wheels |
|---|---:|---:|
| `kyon_quadruped` | no | no |
| `kyon_quadruped_manipulator` | yes | no |
| `kyon_wheeled` | no | yes |
| `kyon_wheeled_manipulator` | yes | yes |

The current source model uses detailed meshes throughout. To keep the dataset
compact, its visual meshes were reduced with topology- and normal-preserving
quadric edge-collapse decimation, targeting 5,000 triangles per unique mesh.
The already simplified source collision meshes are retained unchanged, and
wheel collision geometry remains the cylinder defined by the source xacro.

This source branch includes steering-wheel joints, corrected contact frames and
wheel dimensions, a non-mirrored left-foot mesh, and collision meshes that do
not overlap at the source `home` posture. The resulting `home` configurations
are self-collision free for all four variants.

The source repository does not currently declare a redistribution license: its
`kyon_urdf/package.xml` contains `<license>TODO</license>` and no license file is
provided. This must be resolved with the original maintainers before public
redistribution.
