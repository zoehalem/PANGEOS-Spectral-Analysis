## PANGEOS-Spectral-Analysis
Spectral unmixing, second derivative and statistical analysis of PANGEOS Norway 2025 field spectrometer data. 

Unmixing protocol adapted from Ochoa et al. 2025 https://github.com/emit-sds/SpectralUnmixing.jl
  endmembers == soil at nadir; vegetation at leaf level (taken with SVC RT Sphere)
  mixed == nadir SVC indoor canopy level with 14 degree FOV over 350-2500nm wavelength range

## Unmix spectra formula: 
Leaf Fraction (per wavelength) = mixed - (soil fraction * soil endmember)
Unmixed leaf spectra (per wavelength) = leaf fraction / (1 - soil fraction)

therefore: 

Unmixed leaf spectra = (mixed - (soil fraction * soil endmember)) / (1 - soil fraction)

# Residual error analysis
  # Root Mean Squared Error (RMSE) analysis
  # R^2 and Spectral Angle Mapper (SAM) 
