# Muscle Fiber Model

This document defines the data model for muscle fiber research data, including anatomical, physiological, and biomechanical measurements.

### Muscle

The primary entity representing a muscle with all associated data and measurements.

- __name__
  - Type: string
  - Term: schema:name
  - Description: The anatomical name of the muscle (e.g., "M. tibialis anterior", "Gastrocnemius medialis").

- anatomy
  - Type: string
  - Description: Detailed anatomical description including muscle architecture, fiber arrangement, and location (e.g., "bipennate muscle on the anterior lower leg with fibers arranged at 15° pennation angle").

- function
  - Type: string
  - Description: Primary biomechanical functions and movement contributions (e.g., "dorsiflexion and inversion of the ankle joint, contributes to gait stability during stance phase").

- species
  - Type: [Species](#species)[]
  - Description: List of species from which experimental data has been collected, including sample characteristics and demographics.

- measurement_protocol
  - Type: [Measurement](#measurement)[]
  - Description: Comprehensive list of experimental measurements and protocols performed on this muscle (e.g., force-length relationships, EMG recordings, imaging studies).

- model_3d
  - Type: [Model3D](#model3d)[]
  - Description: Available three-dimensional representations including anatomical meshes, CAD models, and computational simulation models.

- literature
  - Type: [Literature](#literature)[]
  - Description: Curated collection of peer-reviewed publications and research studies related to this muscle.

### Species

Taxonomic and demographic information about the subjects used in muscle research.

- __name__
  - Type: SpeciesType
  - Description: Taxonomic species classification of the experimental subjects.

- strain
  - Type: string
  - Description: Specific genetic strain or subspecies designation (e.g., "Wistar rat", "C57BL/6 mouse"). Optional field for laboratory animals.

- sample_size
  - Type: integer
  - Description: Total number of individual subjects included in the dataset for statistical analysis.

- sex
  - Type: SexType
  - Description: Biological sex distribution of the study subjects.

- measurement_protocol
  - Type: Identifier
  - Description: Reference identifier linking to the specific measurement protocols applied to this species group.

- bodyside
  - Type: string
  - Description: Anatomical side(s) from which data was collected (e.g., "left", "right", "bilateral"). Enables filtering by laterality.

- age
  - Type: string
  - Description: Age classification or specific age range of subjects (e.g., "adult", "juvenile", "P30", "6-8 months", "18-25 years").

- notes
  - Type: string
  - Description: Additional contextual information about the subject population (e.g., "trained athletes", "sedentary controls", "disease model", "post-surgical").

### Measurement

Experimental protocols and data collection methods used to characterize muscle properties.

- __name__
  - Type: string
  - Description: Standardized name or abbreviation for the measurement protocol (e.g., "FLR" for force-length relationship, "FVR" for force-velocity relationship).

- measurement_type
  - Type: string
  - Description: Classification of the experimental approach (e.g., "isotonic", "isokinetic", "isometric", "eccentric", "concentric", "custom protocol").

- parameter
  - Type: [Parameter](#parameter)[]
  - Description: Quantitative parameters and metrics derived from the measurement (e.g., maximum force, optimal length, contraction velocity).

- emg_data
  - Type: [EMGData](#emgdata)[]
  - Description: Electromyographic recordings capturing muscle activation patterns and neural control signals.

- imaging_data
  - Type: [Imaging](#imaging)[]
  - Description: Medical imaging data including structural and functional imaging modalities (MRI, ultrasound, CT scans).

- species_ID
  - Type: Identifier[]
  - Description: Reference identifiers linking measurements to specific species and subject groups.

- raw_data
  - Type: boolean
  - Description: Indicates whether unprocessed, original measurement data is available for download and analysis.

- measurement_date
  - Type: string
  - Description: Date when the experimental measurement was conducted (ISO 8601 format recommended).

### Parameter

Quantitative measurements and calculated metrics derived from experimental data.

- __name__
  - Type: string
  - Term: schema:name
  - Description: Standardized parameter name following established nomenclature (e.g., "F_max" for maximum force, "L_opt" for optimal length, "V_max" for maximum velocity).

- value
  - Type: float[], float
  - Description: Numerical value(s) of the parameter. Supports single values, arrays for multiple measurements, or coordinate pairs for relationships (e.g., 1.25, [1.2, 1.3, 1.4], [{"length": 1.0, "force": 25.0}]).

- unit
  - Type: string
  - Description: Standard unit of measurement following SI conventions (e.g., "N" for force, "m/s" for velocity, "N/m²" for stress).

### EMGData

Electromyographic data capturing muscle electrical activity and activation patterns.

- __type__
  - Type: EMGDataType
  - Description: Method of EMG signal acquisition - surface electrodes or intramuscular fine-wire/needle electrodes.

- electrode_position
  - Type: string
  - Description: Standardized electrode placement description following established guidelines (e.g., "SENIAM standard position", "muscle belly midpoint").

- sampling_rate
  - Type: integer
  - Unit: Hz
  - Description: Digital sampling frequency of the EMG recording system, typically 1000-4000 Hz for research applications.

- raw_data
  - Type: boolean
  - Description: Availability of unfiltered, raw EMG signals for custom processing and analysis.

- processed_data
  - Type: [Parameter](#parameter)[]
  - Description: Derived EMG features and metrics (e.g., RMS amplitude, median frequency, mean power frequency, onset/offset timing).

### Imaging

Medical and research imaging data providing structural and functional muscle information.

- __modality__
  - Type: ImagingModality
  - Description: Imaging technology used for data acquisition, each providing different tissue contrast and information.

- resolution
  - Type: string
  - Description: Spatial resolution specifications (e.g., "1mm isotropic", "512x512 pixels", "0.5mm in-plane, 3mm slice thickness").

- format
  - Type: string
  - Description: Digital file format for image storage and distribution (e.g., "DICOM", "NIfTI", "PNG", "TIFF").

- url
  - Type: string
  - Description: Direct link or persistent identifier for accessing the imaging dataset.

### Model3D

Three-dimensional computational and anatomical models of muscle structure.

- __format__
  - Type: Model3DFormat
  - Description: File format specification for 3D model data, determining compatibility with different software platforms.

- level_of_detail
  - Type: Model3DLevelOfDetail
  - Description: Mesh complexity and anatomical detail level, affecting file size and computational requirements.

- linked_measurement
  - Type: string
  - Description: Reference identifier connecting the 3D model to specific experimental measurements or imaging data used for model creation.

- source
  - Type: string
  - Description: Methodology used for model generation (e.g., "MRI segmentation", "micro-CT reconstruction", "CAD design", "photogrammetry").

### Literature

Peer-reviewed publications and research documentation related to muscle studies.

- __doi__
  - Type: Identifier
  - Term: schema:identifier
  - Description: Digital Object Identifier providing persistent, unique reference to the publication for citation and access.
  - XML: @doi

- title
  - Type: string
  - Term: schema:name
  - Description: Complete title of the research publication or article.

- authors
  - Type: [Author](#author)[]
  - Term: schema:author
  - Description: Ordered list of all contributing authors with their institutional affiliations and contact information.

- publication_year
  - Type: integer
  - Term: schema:datePublished
  - Description: Year of publication in peer-reviewed journal or conference proceedings.
  - Minimum: 1900
  - Maximum: 2100

- citations
  - Type: integer
  - Term: schema:citation
  - Description: Number of times this publication has been cited by other research works, indicating scientific impact.
  - Default: 0

### Author

Individual researcher or scientist contributing to published muscle research.

- __name__
  - Type: string
  - Term: schema:name
  - Description: Full name of the author as it appears in the publication (e.g., "Dr. Jane Smith", "John A. Doe").

- __email__
  - Type: string
  - Term: schema:email
  - Description: Professional email address for correspondence and collaboration inquiries.

## Enumerations

### SpeciesType

```python
HUMAN = "human"
RAT = "rat"
MOUSE = "mouse"
RABBIT = "rabbit"
PIG = "pig"
MACAQUE = "macaque"
DOG = "dog"
CAT = "cat"
OTHER = "other"
```

### SexType

```python
MALE = "male"
FEMALE = "female"
MIXED = "mixed"
UNKNOWN = "unknown"
```

### Model3DFormat

```python
STL = "STL"
OBJ = "OBJ"
GLTF = "GLTF"
FBX = "FBX"
PLY = "PLY"
STEP = "STEP"
```

### Model3DLevelOfDetail

```python
LOW = "low"
MEDIUM = "medium"
HIGH = "high"
ULTRA_HIGH = "ultra-high"
```

### ImagingModality

```python
MRI = "MRI"
CT = "CT"
ULTRASOUND = "Ultrasound"
X_RAY = "X-ray"
DTI = "DTI"
FMRI = "fMRI"
```

### EMGDataType

```python
SURFACE = "surface"
INTRAMUSCULAR = "intramuscular"
```
