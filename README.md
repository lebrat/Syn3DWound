# Syn3DWound Dataset

## Overview
Syn3DWound is a high-fidelity synthetic dataset for 3D wound bed analysis, introduced in the paper "Syn3DWound: A Synthetic Dataset for 3D Wound Bed Analysis".
It generates realistic 2D images and precise 3D models of chronic wounds (e.g., pressure, trauma, arterial) on 3D human avatars using Blender's Cycles renderer, addressing the lack of diverse 3D training data for wound segmentation and reconstruction. 
Key features include controlled variations in camera trajectories, lighting (strong/weak), image degradations (blur, motion blur), and perfect 2D/3D ground truth annotations like segmentation masks, camera intrinsics/extrinsics, and meshes—ideal for benchmarking NeRF, COLMAP, and segmentation models in biomedical AI.

## Data Structure
Files follow a naming convention: subject\_\<ID\>/Syn3DWound\_\<Wound_ID\>\_\<body_part\>\_lighting\_\<angle\>
```text
Syn3DWound/
├── subject_1/ # Subject 1 raw or base data
├── subject_2/ # Subject 2 raw or base data
	├── Syn3DWound_0415_leg_strong_lighting_phi/ # 3D object data for leg wound under strong lighting (phi view)
	├── Syn3DWound_0534_foot_weak_lighting_theta/ # 3D object data for foot wound under wak lighting (theta view)
		├── BB.txt # Bounding box annotations
		├── cropped_mesh.obj.txt # Cropped mesh object file
		├── images/ # Original images
		├─── images_blurred/ # Blurred images (for robustness testing)
		├── images_motion_blurred/ # Motion-blurred images (for robustness testing)
		├── mask/ # Segmentation masks (strong lighting, phi view)
		└── simon_0534_foot_weak_lighting_theta_colmap/ # COLMAP files
```

## Acquisition and Processing
Generated from real 2D wound images sculpted onto avatars (e.g., RenderPeople, 3D BodyTex datasets) with manual depth carving.
Rendered with Cycles for photorealism (path-traced, ~13s/4K image on RTX 2080Ti cluster); includes camera poses, lighting controls, and augmentations (blur, overexposure).Supports diverse body shapes, skin tones, wound types/locations (leg ID0415, foot ID0534); outperforms game engines in realism.

## Intended Use
- Train/test 3D reconstruction models (e.g., COLMAP, Meshroom, NeRF, Gaussian Splatting).
- 2D/3D wound segmentation (e.g., SegFormer)
- Lighting/pose-robust models for clinical wound morphometry (volume, depth).
- Research wound assessment in clinical settings (non-diagnostic).

## Citation
```bibtex
@article{lebrat2023syn3dwound,
  title={Syn3DWound: A Synthetic Dataset for 3D Wound Bed Analysis},
  author={Lebrat, L{\'e}o and Cruz, Rodrigo Santa and Chierchia, Remi and Arzhaeva, Yulia and Armin, Mohammad Ali and Goldsmith, Joshua and Oorloff, Jeremy and Reddy, Prithvi and Nguyen, Chuong and Petersson, Lars and others},
  journal={arXiv preprint arXiv:2311.15836},
  year={2023}
}
```
