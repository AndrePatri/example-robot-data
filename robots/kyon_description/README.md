# Kyon

Source: https://github.com/ADVRHumanoids/iit-kyon-ros-pkg

Source branch: `primitive_collisions` (based on `ros2`)

Source revision: `f356fbfe0d072a009ee46aa63302bb0908157e77`

Simplified collision meshes: `crzz-dev` revision
`6b98cb0` (introduced by `b9f6d4b`).

The four static descriptions are generated from `kyon_urdf/urdf/kyon.urdf.xacro`
and `kyon_srdf/srdf/kyon.srdf.xacro`. All variants use the legs and explicitly
include the 9.8 kg Varta battery; cameras, lidar, the alternative D034 battery,
payloads, and the xacro floating joint are disabled. The free-flyer is added by
the Example Robot Data loader. Following the current source description, the
upper-body variants include the Dagana hand assemblies.

The Varta selection is explicit because the source now defaults both battery
options to off. Its mass has not been folded into the 19.962822 kg pelvis body;
the selected battery remains a separate inertial link in the source model.

| Description | Upper body | Wheels |
|---|---:|---:|
| `kyon_quadruped` | no | no |
| `kyon_quadruped_manipulator` | yes | no |
| `kyon_wheeled` | no | yes |
| `kyon_wheeled_manipulator` | yes | yes |

These four names use the lightweight primitive collision model. Append
`_mesh` to any name (for example, `kyon_wheeled_manipulator_mesh`) to load the
same robot with the approximately 100-triangle collision meshes from the
source `crzz-dev` branch. The model choice is made at load time and does not
introduce runtime conversion or duplicated model data.

To keep the dataset compact, most visual meshes were reduced with topology-
and normal-preserving quadric edge-collapse decimation, targeting 5,000
triangles per unique mesh. The pelvis visual is retained at source resolution:
it contains hundreds of separate components, and whole-mesh decimation visibly
corrupts its surface.

Primitive collision geometry uses fitted boxes for the links. Hip-roll
collision is omitted because the pelvis and hip-pitch shapes already cover that
region. The simplified 100-triangle pelvis collision mesh is the sole exception
in the primitive variants: its iDCOL convex-poly conversion is tractable,
whereas its enclosing box creates false pelvis--shoulder collisions in the
nominal upper-body pose. The `_mesh` variants use the simplified link meshes,
including hip roll. Wheels remain analytic cylinders in both representations
so their collision geometry is rotationally symmetric.

This source branch includes revised inertial properties, steering-wheel
kinematics, foot/contact-frame placement, collision meshes, and reference
configurations. The generated descriptions deliberately retain continuous
wheel joints: representing an unbounded wheel by a revolute joint with
artificial +/-1e9 radian limits changes its configuration manifold and creates
meaningless position limits for downstream optimal-control code.

The source repository does not currently declare a redistribution license: its
`kyon_urdf/package.xml` contains `<license>TODO</license>` and no license file is
provided. This must be resolved with the original maintainers before public
redistribution.
