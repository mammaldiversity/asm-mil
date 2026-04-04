# Contribting to this project

## Pre-requisites

Requirements for development:

- [mil-kit](https://pypi.org/project/mil-kit/)
- [python 3.10+](https://www.python.org/downloads/)

To intall mil-kit, run the following command:

```bash
pip install mil-kit
```

If you are using [uv](https://astral.sh/uv/) for Python version management, you can create a virtual environment and install the dependencies as follows:

```bashbash
uv venv
uv pip install mil-kit
```

## Release process

### Convert the PSD files release by the ASM MIL committee to webp format. It will also remove all the non-image layers.

Run the following command to convert the PSD files to webp format:

```bash
uv run mil-kit export -d path/to/psd/files -r --max-resolution 540 -o path/to/webp/output -f webp
```

> **Important**: Make sure to set the `--max-resolution` flag to `540` to ensure that the images are resized to a maximum resolution supported by the ASM MDD website.

### Generate watermarked images for the web catalog

Run the following command to generate watermarked images for the web catalog:

```bash
uv run mil-kit watermark -d path/to/webp/output -r -o watermark-540px -m path/to/mil/excel/metadata -f webp
```

### Copy the watermarked images to the this repository

Run the following command to copy the watermarked images to this repository:

```bash
cp -r watermark-540px/*.webp images-540px-webp/
```

### Update the metadata

After copying the watermarked images to this repository, you will need to update the metadata for the images. The metadata is stored in the `metadata` directory in this repository. You only need to copy the metadata provided by the ASM MIL committee to the `metadata` directory in this repository. Remove the old metadata files before copying the new ones to avoid confusion.

```bash
rm -rf metadata/*
cp -r path/to/mil/excel/metadata.xlsx metadata/
```

### Commit and push the changes to this repository

After updating the images and metadata, commit and push the changes to this repository:

```bashgit add .
git commit -m "Update images and metadata for the ASM MIL web catalog"
git push origin main
```

### Add tags and release on GitHub

The release process is automated using GitHub Actions. To trigger the release process, you need to add a tag to the latest commit and push it to GitHub. The tag should follow the format v{year}-{month}-{day} (e.g., v2024-06-01).

For example, to add a tag and push it to GitHub, run the following commands:

```bash
git tag v2024-06-01
git push origin --tag
```
