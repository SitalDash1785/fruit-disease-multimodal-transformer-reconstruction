# GitHub Upload Guide

This guide uploads the reconstructed package as a public or private GitHub repository. It does not publish the study dataset.

## 1. Review the package first

Before publication:
- Replace placeholder feature names, class count and paths only with verified study details.
- Review the provenance note and retain it.
- Do not add private datasets, credentials, access tokens, participant information or unapproved model checkpoints.
- Do not claim that this reconstructed package is the original code or that it reproduces the manuscript's reported results.

## 2. Create a repository

1. Sign in to GitHub.
2. Select **New repository**.
3. Suggested repository name: `fruit-disease-multimodal-transformer-reconstruction`.
4. Add the description shown in `REPOSITORY_DESCRIPTION.txt`.
5. Choose **Public** only if the code and all included materials are approved for public release; otherwise choose **Private**.
6. Do not initialize with a README if you are uploading this complete package, because it already contains one.
7. Create the repository.

## 3. Upload through the GitHub website

1. Extract `Fruit_Disease_Reproducibility_Package.zip` on your computer.
2. Open the newly created empty repository.
3. Select **Add file → Upload files**.
4. Drag the extracted package contents into the upload area. Upload the files and folders, not the ZIP file alone.
5. Check that `README.md`, `src/`, `configs/`, `DATA_SCHEMA.md` and `CODE_PROVENANCE.txt` appear in the upload list.
6. Enter a commit message such as `Add reconstructed reproducibility scaffold`.
7. Select **Commit changes**.

## 4. Verify the repository

After upload, check that:
- the README renders correctly;
- all scripts and configuration files are present;
- no dataset, credentials or private paths were accidentally included;
- the provenance and limitations are visible;
- the repository visibility matches the intended release.

## 5. Add the repository link to the manuscript

Copy the actual repository URL from your browser only after the repository has been created and reviewed. Do not invent a URL or cite a repository that is not yet publicly accessible. If the repository is private, confirm that the journal and reviewers can access it before stating that it is publicly available.

## Optional command-line upload

If Git is installed, open a terminal in the extracted package folder and run:

```bash
git init
git add .
git commit -m "Add reconstructed reproducibility scaffold"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

Replace the remote URL with the actual URL of the repository you created. Never paste a personal access token into a script, README or manuscript.
