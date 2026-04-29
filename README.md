# MIA Project 2: Valve Artifact Detection

## Goal

This project detects shunt valve artifacts in 3D MRI scans.

Each subject contains:
- an MRI image volume
- a ground-truth valve artifact mask
- a catheter mask
- a JSON metadata file

The goal for Task A is to generate a binary artifact mask:

- `0` = not artifact
- `1` = valve artifact

## Current Progress

So far, we have:

1. Set up the project folder.
2. Loaded one training subject in Python.
3. Loaded the MRI volume using `nibabel`.
4. Loaded the ground-truth artifact mask.
5. Visualized MRI slices with the artifact mask overlaid.

This lets us understand what the valve artifact looks like before building an automatic method.

## Current Pipeline Idea

We are avoiding deep learning for now and using a classical image-processing pipeline.

Planned steps:

1. Load the MRI volume.
2. Normalize image intensities.
3. Threshold extreme bright and dark voxels.
4. Remove small noisy regions using connected components.
5. Keep likely artifact regions.
6. Clean the mask using morphology.
7. Save the predicted binary mask as `.nii.gz`.

## Why This Works

The valve contains metal, which creates abnormal MRI artifacts. These artifacts often appear as unusual bright or dark regions near the skull. Because they look different from normal brain tissue, we can start with intensity thresholding and cleanup operations.

## Folder Structure

```text
data/
    train/
        subj001/
            subj001_image.nii.gz
            subj001_artifact.nii.gz
            subj001_catheter.nii.gz
            subj001.json

notebooks/
    explore_artifacts.ipynb

src/
    future reusable code

outputs/
    predicted masks