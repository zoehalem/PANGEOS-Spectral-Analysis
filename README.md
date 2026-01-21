# PANGEOS-Spectral-Analysis
Spectral unmixing, second derivative and statistical analysis of PANGEOS Norway 2025 field spectrometer data. 

## Preprocessing
Begin by preprocessing spectral data. Steps include interpoation, water band removal, interpolation, overlap matching, jump correction, conversion to absolute reflectance, and signal smoothing. 
The preprocessing script (field_spectra_processing.ipynb) can be adjusted depending on which steps you would like to include. 

## Spectral Unmixing
Unmixing protocol adapted from Ochoa et al. 2025 https://github.com/emit-sds/SpectralUnmixing.jl
  endmembers = soil at nadir; vegetation at leaf level (taken with SVC RT Sphere)
  
  mixed = nadir SVC indoor canopy level with 14 degree FOV over 350-2500nm wavelength range

There are two unmixing scripts, one using all the endmember data and all mixed spectra (unmixed_leaf_spectra.ipynb), and another using only plots 1108, 1310 and 1405 (unmixed_leaf_spectra_limited.ipynb) which includes only plots where we have both nadir and leaf level measurements. 

### Unmix spectra formula: 

Leaf Fraction (per wavelength) = mixed - (soil fraction * soil endmember)

Unmixed leaf spectra (per wavelength) = leaf fraction / (1 - soil fraction)

therefore: 

Unmixed leaf spectra = (mixed - (soil fraction * soil endmember)) / (1 - soil fraction)

## Residual error analysis
Evaluating the robustness of the unmixing model

### Root Mean Squared Error (RMSE) analysis
Simulated spectra are generated using the following formula to compare with the mixed spectra: 

Simulated spectrum = (1 - % soil) * average leaf endmember + % soil * average soil endmember

Simulated and mixed spectra RMSEs are compared, as well as unmixed and mixed spectra RMSEs (RMSE_analysis.ipynb). 

### R^2 and Spectral Angle Mapper (SAM) 
R^2 and Spectral Angle Mapper (SAM) are employed for unmixing model robustness (R2_SAM_analysis.ipynb). 
There are two methods for R^2 calculations: 

R^2 = 1 − (∑(a − b)^2) / (∑(b − a)^2)

which treats the unmixed spectrum (a) as a prediction and the reference endmember (b) as the "truth". This technique is sensitive to absolute scaling, therefore differences in absolute reflectance can cause poor R^2 values. 

and 

b ≈ β0 + β1 * a

which computes R^2 as a linear regression of b on a, and and ignores absolute reflectance (magnitude) differences. This technique may therefore overestimate fit quality, and even when the R^2 value is high, the unmixing model can still remove important spectral features present in the original mixed spectrum. 

## PCA and LDA
Unsupervised (PCA) and supervised (LDA) analysis on mixed spectral data (no unmixing algorithm applied) (stat_analysis.ipynb). 
Additionally, the same statistical analysis is performed on the second derivative data (stat_analysis-2dr.ipynb). 
