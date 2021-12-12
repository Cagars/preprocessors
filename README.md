# Preprocessors

Preprocessors to remove DICOM masks and generate segmentations.

### Prepare Dependencies
```
pip install opencv-python pydicom matplotlib pandas
```

### Command Usage
```
usage: main.py [-h] --dcm-dir DCM_DIR 
                    --label-dir LABEL_DIR 
                    --target-dir TARGET_DIR 
                    --mode {inspector,mask,roi,spreadsheet}
                    [--new-shape NEW_SHAPE]
                    [--jobs JOBS]

This is a preprocessor to remove DICOM masks and generate segmentations and
its inspectors, masks and ROIs.

optional arguments:
  -h, --help            show this help message and exit
  --dcm-dir DCM_DIR     The DICOM root directory
  --label-dir LABEL_DIR
                        The JSON labels root directory
  --target-dir TARGET_DIR
                        The destination root directory for outputs
  --mode {inspector,mask,roi,spreadsheet}
                        inspector    Generate four-in-one images to compare masks, overlay 
                                     and noise-eliminated with original image
                        mask         Generate binary masks that will be used as Dataset
                                     for segmentation models
                        roi          Generate region-of-interest images that will be used 
                                     as Dataset for classification model
                        spreadsheet  Generate CSV files that contains encrypted
                                     patients identifiers and its file name
  --new-shape NEW_SHAPE
                        WxH. Resize the output image with desired width and height
  --jobs JOBS           Number of workers
```
```
usage: assign.py [-h] --csv-file CSV_FILE 
                      --source-dirs SOURCE_DIRS
                      --target-dir TARGET_DIR

This is an assigner for assigning dataset validation job fairly.

optional arguments:
  -h, --help            show this help message and exit
  --csv-file CSV_FILE   The assignees CSV file
  --source-dirs SOURCE_DIRS
                        dir1,dir2,dir3,..  The source directories to be assigned to
  --target-dir TARGET_DIR
                        The destination directory where the assigned directory will be located
```

### Dataset Hierarchy
```
Dataset:
- {LABEL_DIR}
    - *
        - ENDO
            - *.json
- {DCM_DIR}
    - *
        - ENDO
            - *.dcm
```