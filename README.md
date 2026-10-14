# Construction of a Multiview Colored Point Cloud Dataset of Postharvest Lychee Clusters

**Download the complete dataset:** [v1.0](https://github.com/Haikun0619/Lychee_point_cloud_dataset/releases/tag/v1.0)

On the release page, download the dataset archive under **Assets**. Extract the archive to obtain the complete directory structure.

## Overview

This dataset contains multiview colored point clouds of postharvest `Yuhebao` lychee clusters acquired under controlled conditions. It preserves the relationships among samples, leaf states, acquisition distances, and measured cluster attributes. The dataset comprises 5,760 cropped PLY files from 80 lychee clusters.

Each cluster was recorded with and without leaves at acquisition distances of 40, 45, and 50 cm. Twelve point clouds were extracted from each recording at fixed time intervals. Records of the same cluster under different leaf states and acquisition distances can be grouped by sample identifiers. The 12 point clouds from each recording are numbered in extraction order.

## Dataset Highlights

| Item | Value |
|---|---:|
| Lychee cultivar | `Yuhebao` |
| Number of clusters | 80 |
| Leaf states | With leaves and without leaves |
| Acquisition distances | 40, 45, and 50 cm |
| Point clouds extracted per recording | 12 |
| Acquisition records per cluster | 6 |
| Total acquisition records | 480 |
| PLY files per distance × leaf-state combination | 960 |
| Total cropped colored point clouds | 5,760 |
| Point-cloud format | PLY |

## Acquisition Setup

Data were acquired with an Intel RealSense D435i depth camera mounted on a controlled multiview apparatus. During acquisition, the lychee cluster remained stationary while the camera and a black background panel rotated synchronously around it. An auxiliary light was used to maintain consistent illumination.

The apparatus had a length of approximately 1,444.10 mm, a width of 572.75 mm, and a height of 855.00 mm. The rotary stage supported a 360° travel range, a maximum angular speed of 25°/s, and a repeat positioning accuracy of 0.005°. During recording, the camera moved at approximately 6°/s and completed one revolution in approximately 60 s.

Each cluster was acquired under the following six conditions:

- With leaves at 40 cm
- With leaves at 45 cm
- With leaves at 50 cm
- Without leaves at 40 cm
- Without leaves at 45 cm
- Without leaves at 50 cm

## Point-Cloud Processing

To select data from periods of stable apparatus operation, some frames at the beginning and end of each recording were excluded. Twelve colored point clouds were then extracted from the retained data at fixed time intervals and spatially cropped to retain the region containing the lychee cluster. Each cropped result was saved as a separate PLY file.

Each PLY file contains three-dimensional point coordinates and the corresponding color information.

## Directory Organization

The dataset is organized first by leaf state and then by acquisition distance:

```text
Lychee_point cloud_dataset/
├── T/                              # With leaves
│   ├── 40/
│   │   └── <sample_directory>/
│   │       ├── cloud_0001.ply
│   │       ├── cloud_0002.ply
│   │       ├── ...
│   │       └── cloud_0012.ply
│   ├── 45/
│   └── 50/
└── F/                              # Without leaves
    ├── 40/
    ├── 45/
    └── 50/
```

`T` denotes a cluster recorded with leaves, and `F` denotes the same cluster recorded after leaf removal. Each sample directory contains 12 PLY files, numbered in the order in which the point clouds were extracted from that recording.

## Sample Directory Naming

The fields in each sample directory name follow this order:

```text
<batch_id>-<cluster_id>-<distance>-<leaf_state>-<mass>-<fruit_count>-<horizontal_span>-<vertical_span>
```

| Field | Description | Unit or allowed value |
|---|---|---|
| `batch_id` | Acquisition batch identifier | Identifier |
| `cluster_id` | Lychee cluster identifier within the batch | Identifier |
| `distance` | Camera-to-target acquisition distance | `40`, `45`, or `50` cm |
| `leaf_state` | Leaf condition during acquisition | `T` or `F` |
| `mass` | Cluster mass recorded for the corresponding leaf state | g |
| `fruit_count` | Number of fruits in the cluster | Count |
| `horizontal_span` | Maximum horizontal span of the cluster | cm |
| `vertical_span` | Maximum vertical span of the cluster | cm |

The `batch_id` and `cluster_id` remain unchanged across leaf states and acquisition distances. These two fields should be used together to group all records belonging to the same lychee cluster.

## Experimental Unit and Paired Records

The directory structure supports several levels of analysis:

- **Cluster level:** 80 independent lychee clusters.
- **Condition level:** six acquisition records per cluster, formed by two leaf states and three distances.
- **Point cloud record level:** 12 sequentially numbered PLY files per acquisition record.

## Sample Characteristics

- Fruit count ranges from 2 to 15 fruits per cluster.
- With leaves, mean mass is 132.10 g, standard deviation is 59.83 g, and median mass is 109.02 g.
- Without leaves, mean mass is 125.49 g, standard deviation is 58.19 g, and median mass is 103.75 g.

## Quality Checks

All 5,760 PLY files were checked before release. The checks confirmed that:

- every distance × leaf-state combination contains 960 PLY files;
- each acquisition record contains PLY files numbered 1–12 with no missing or duplicate entries;
- all PLY files can be read successfully;
- no empty point clouds were found;
- no invalid three-dimensional coordinates were found;
- point coordinates and color information are present and correspond correctly; and
- directory names are consistent with the sample records.

## Potential Research Uses

The dataset may support research on:

- multiview point-cloud registration and fusion;
- three-dimensional reconstruction;
- point-cloud completion;
- analysis of leaf occlusion and acquisition distance;
- lychee-cluster dimension measurement;
- cluster-mass estimation using point-cloud and sample attributes; and
- methods that jointly use geometry, color, fruit count, and physical measurements.

## Known Limitations

- The dataset was collected with a controlled experimental apparatus and does not reproduce the illumination, background, cluster state, or camera operation of a natural orchard.
- Only the `Yuhebao` cultivar is included.
- Occlusion, object boundaries, fruit stalks, and thin branches may contain local point loss or geometric distortion.
- Multiview acquisition records visible surfaces from different directions but does not guarantee complete coverage of every surface inside a cluster.

## Data Access

- **Current version:** v1.0
- **Release date:** October 14, 2026

## Funding

This work was supported by the Scientific Research Startup Fund of Guangdong Ocean University (grant number YJR24018) and the Zhanjiang Non-Funded Science and Technology Research Project (grant number 2025B01137).

## Contact

- **Dataset maintainer:** Haikun Zheng
- **Institution:** Guangdong Ocean University
- **Email:** haikun0619@gmail.com
