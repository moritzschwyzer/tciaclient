<!--

#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: index.ipynb
# command to build the docs after a change: nbdev_build_docs

-->

# TCIA (The Cancer Imaging Archive) Download Client for Python

> This Python package uses the official TCIA REST API to enable downloads from www.cancerimagingarchive.net from within Python scripts and Jupyter Notebooks.


The documentation can be found at https://moritzschwyzer.github.io/tciaclient/.

## Install

`pip install tciaclient`

## How to use

Step 1: Import the `TCIAClient` from the `tciaclient.core` package.
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
from tciaclient.core import TCIAClient
```

</div>

</div>

Step 2: Create an instance of the `TCIAClient`.
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
tc = TCIAClient()
```

</div>

</div>

Step 3: Choose a collection name from https://wiki.cancerimagingarchive.net/display/Public/Collections.
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
collection_name = "NSCLC-Radiomics"
collection = tc.get_patient(collection_name)
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
import pandas as pd
collection_df = pd.DataFrame(collection); collection_df.head()
```

</div>
<div class="output_area" markdown="1">




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PatientID</th>
      <th>PatientName</th>
      <th>PatientSex</th>
      <th>Collection</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>LUNG1-001</td>
      <td>LUNG1-001</td>
      <td>M</td>
      <td>NSCLC-Radiomics</td>
    </tr>
    <tr>
      <td>1</td>
      <td>LUNG1-007</td>
      <td>LUNG1-007</td>
      <td>M</td>
      <td>NSCLC-Radiomics</td>
    </tr>
    <tr>
      <td>2</td>
      <td>LUNG1-029</td>
      <td>LUNG1-029</td>
      <td>F</td>
      <td>NSCLC-Radiomics</td>
    </tr>
    <tr>
      <td>3</td>
      <td>LUNG1-036</td>
      <td>LUNG1-036</td>
      <td>F</td>
      <td>NSCLC-Radiomics</td>
    </tr>
    <tr>
      <td>4</td>
      <td>LUNG1-056</td>
      <td>LUNG1-056</td>
      <td>F</td>
      <td>NSCLC-Radiomics</td>
    </tr>
  </tbody>
</table>
</div>



</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
for c in collection:
    c["PatientID"]
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
studies = tc.get_patient_study(collection=collection_name, patientId=collection[0]["PatientID"])
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
studies
```

</div>
<div class="output_area" markdown="1">




    [{'Collection': 'NSCLC-Radiomics',
      'PatientID': 'LUNG1-001',
      'PatientName': 'LUNG1-001',
      'PatientSex': 'M',
      'StudyInstanceUID': '1.3.6.1.4.1.32722.99.99.239341353911714368772597187099978969331',
      'StudyDate': '2008-09-18',
      'PatientAge': '083Y',
      'SeriesCount': 3}]



</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
series = tc.get_series(studyInstanceUid=studies[0]["StudyInstanceUID"])
```

</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
series
```

</div>
<div class="output_area" markdown="1">




    [{'PatientID': 'LUNG1-001',
      'StudyInstanceUID': '1.3.6.1.4.1.32722.99.99.239341353911714368772597187099978969331',
      'SeriesInstanceUID': '1.3.6.1.4.1.32722.99.99.298991776521342375010861296712563382046',
      'Modality': 'CT',
      'ProtocolName': 'RCCTPET_THORAX_CONTRAST_dag0',
      'SeriesDate': '2008-09-18',
      'BodyPartExamined': 'LUNG',
      'SeriesNumber': '0.000000',
      'Collection': 'NSCLC-Radiomics',
      'Manufacturer': 'SIEMENS',
      'ManufacturerModelName': 'Biograph 40',
      'SoftwareVersions': 'syngo CT 2006A',
      'Visibility': '1',
      'ImageCount': 134},
     {'PatientID': 'LUNG1-001',
      'StudyInstanceUID': '1.3.6.1.4.1.32722.99.99.239341353911714368772597187099978969331',
      'SeriesInstanceUID': '1.2.276.0.7230010.3.1.3.2323910823.20524.1597260509.554',
      'Modality': 'SEG',
      'SeriesDate': '2020-08-12',
      'SeriesDescription': 'Segmentation',
      'BodyPartExamined': 'LUNG',
      'SeriesNumber': '300.000000',
      'Collection': 'NSCLC-Radiomics',
      'Manufacturer': 'QIICR',
      'ManufacturerModelName': 'https://github.com/qiicr/dcmqi.git',
      'SoftwareVersions': '3efde87',
      'Visibility': '1',
      'ImageCount': 1},
     {'PatientID': 'LUNG1-001',
      'StudyInstanceUID': '1.3.6.1.4.1.32722.99.99.239341353911714368772597187099978969331',
      'SeriesInstanceUID': '1.3.6.1.4.1.32722.99.99.227938121586608072508444156170535578236',
      'Modality': 'RTSTRUCT',
      'SeriesNumber': '3.000000',
      'Collection': 'NSCLC-Radiomics',
      'Manufacturer': 'Varian Medical Systems',
      'ManufacturerModelName': 'ARIA RadOnc',
      'SoftwareVersions': '15.5.11',
      'Visibility': '1',
      'ImageCount': 1}]



</div>

</div>
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
tc.get_image(seriesInstanceUid = z[0]["SeriesInstanceUID"],
             downloadPath  ="./", zipFileName ="images.zip")
```

</div>
<div class="output_area" markdown="1">




    True



</div>

</div>
