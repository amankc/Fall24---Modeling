
# ECCO (Estimating the Circulation and Climate of the Ocean) Model
![ECCO logo](pictures/ecco-logo.png)
Understanding ocean circulation and its influence on climate systems is critical, particularly in the face of a changing climate (DeVries, 2014; DeVries et al., 2019). Temperature and salinity are the primary drivers of global ocean currents, regulating the distribution of heat and nutrients throughout the oceans (Riebesell et al., 2007). These processes are essential not only for sustaining marine ecosystems—from microscopic plankton to the largest marine mammals—but also for shaping global weather patterns (Landschützer et al., 2015).

In a warming climate, the heat stored in the ocean’s layers becomes increasingly significant. This heat transport directly impacts polar regions, influencing the melting rates of marine-terminating glaciers and icebergs, the extent and longevity of sea ice, and the habitat suitability for polar species. These changes, in turn, have profound implications for indigenous communities, whose traditions and livelihoods are intricately tied to stable polar environments (Bakker et al., 2014; Pfeil et al., 2013).

The cascading effects of changing ocean conditions are far-reaching, contributing to sea-level rise and affecting key systems such as the Atlantic Meridional Overturning Circulation (AMOC), which regulates the global climate. Furthermore, rising ocean temperatures have intensified the frequency and severity of tropical storms and hurricanes. Areas of warming, illustrated by red regions in Figure 1, highlight zones where ocean temperatures have risen significantly in recent decades. These regions often coincide with the paths of destructive hurricanes and cyclones, fueled by warm ocean waters (Bates et al., 2014; Dore et al., 2009; Feely et al., 2006).

![Ocean heat trend in the upper 200 meters](pictures/ocean-heat-trend.png)
"\n"*Fig 1: Illustration of warming trends in the upper 200 meters of the ocean, highlighting areas with significant temperature increases.*

## Model Description:

ECCO is a state-of-the-art global ocean data assimilation model designed to estimate the time-evolving state of the ocean. It combines a numerical ocean circulation model (MIT-gcm) with observational data through adjoint-based optimization (refer to Fig. 2). This approach minimizes the mismatch between the model output and observations while ensuring that physical laws like conservation of mass and momentum are respected.

MITgcm is a numerical model designed for the study of the atmosphere, ocean, and climate with a flexible non-hydrostatic formulation that enables it to efficiently simulate fluid phenomena over a wide range of scales.

![Schematic illustration of a forward model and its adjoint](pictures/forward-adjoint-model.png)
*Fig: 2 schematic illustration of a forward model and its adjoint. Note the input and output being opposite between the two model (Credit: ECCO v4)*
The model uses the MITgcm (MIT General Circulation Model) as its core, which solves the primitive equations governing ocean and sea-ice dynamics. Key processes represented in ECCO include:

- **Advection and diffusion of tracers** (e.g., temperature, salinity)
- **Ocean-ice-atmosphere interactions**
- **Tidal forcing and its impact on circulation**

### Main Outputs:

#### Ocean + Sea-Ice:
- Ocean temperature, salinity, and velocity
- Sea-ice and snow
- Lateral and vertical fluxes of volume, heat, salt, and momentum

#### Atmosphere:
- Radiative fluxes
- Air-sea-ice-ocean fluxes of heat, moisture, energy, and momentum

## Data Needs:
ECCO relies on a diverse set of observational datasets:

### Satellite Data:
- Altimetry (e.g., TOPEX/Poseidon)
- Sea surface temperature (e.g., MODIS)
- Sea surface salinity

### In Situ Data:
- Argo floats
- Moorings
- Ship-based measurements

### Atmospheric Forcing:
- Wind stress
- Precipitation
- Heat fluxes from reanalysis products (e.g., ERA5)

### Observational Data Used to Constrain the Model:

| Observation Type            | Dataset/Source                                                                 |
|-----------------------------|------------------------------------------------------------------------------|
| Sea surface height          | ERS-1/2, TOPEX/Poseidon, Jason series, CryoSat-2, etc.                       |
| Global mean sea level       | AVISO, CSIRO, NOAA, U.Colorado                                               |
| In situ temperature         | Argo floats, CTDs, XBTs, marine mammals, etc.                               |
| In situ salinity            | CTDs, moorings, Argo floats, etc.                                           |
| Sea surface temperature     | AVHRR                                                                       |
| Sea surface salinity        | Aquarius                                                                    |
| Sea-ice concentration       | SSM/I, SSMIS                                                                |
| Ocean bottom pressure       | GRACE                                                                       |
| T and S climatology         | World Ocean Atlas 2009                                                      |
| Mean dynamic topography     | DTU17MDT                                                                    |

![a) Scientist deploying an ARGO float b) Principle of ARGO float](pictures/argo-floats.png)
*Fig3: (a) Scientist deploying an ARGO float (b) principle of ARGO float (Credit: Scripps Institution of Oceanography, UC San Diego)*

![Instrumented Seal(pictures/seal-instrumentation.png)
Fig4: Instrumented Seal (Credit: NOAA)

## Calibration:

### Physical Parameters:

1. **Vertical Mixing Coefficients:**
   - Governs the vertical exchange of tracers (e.g., heat, salt) and momentum.
   - **Calibration Need:** Adjust to match observed temperature and salinity profiles.
   - **Target Observations:** Argo floats, CTD profiles.

2. **Horizontal Diffusion Coefficients:**
   - Represents lateral mixing of tracers.
   - **Calibration Need:** Ensure tracer transport reflects observed currents and mixing.
   - **Target Observations:** Drifter data and satellite-derived tracer distributions.

3. **Surface Boundary Conditions:**
   - Includes wind stress, heat fluxes, and freshwater fluxes.
   - **Calibration Need:** Correct biases in ocean-atmosphere interactions.
   - **Target Observations:** Satellite-derived wind fields and reanalysis heat flux data.

### Dynamical Parameters:

1. **Sea Surface Height (SSH) Gradients:**
   - Related to geostrophic flow.
   - **Calibration Need:** Match simulated SSH anomalies to satellite altimetry data.
   - **Target Observations:** Altimeter datasets.

2. **Tidal Forcing Amplitudes:**
   - Influence regional dynamics near coasts and shallow seas.
   - **Calibration Need:** Ensure accuracy in tidal mixing and residual flows.
   - **Target Observations:** Tide gauge measurements.

### Numerical Parameters:

1. **Time Step and Grid Resolution:**
   - Affect the stability and accuracy of simulations.
   - **Calibration Need:** Ensure CFL condition is met without excessive computational cost.

2. **Advection and Diffusion Schemes:**
   - Solves tracer transport equations.
   - **Calibration Need:** Prevent artificial diffusion or numerical oscillations.

## Numerical Experiment Design:

### Initial Conditions:
- **Temperature and Salinity:**
  - Start with observed global distributions (e.g., World Ocean Atlas).

- **Sea Surface Height (SSH):**
  - Use satellite altimetry observations.

- **Currents:**
  - Initialize using velocity fields from ECCO reanalysis.

### Boundary Conditions:

#### Surface:
- Wind Forcing: Wind stress from atmospheric reanalysis (e.g., ERA5).
- Heat Fluxes: Solar radiation, latent, and sensible heat fluxes.
- Precipitation/Evaporation: Surface freshwater fluxes from rain, evaporation, and rivers.

#### Lateral (Edges):
- Conditions for temperature, salinity, currents, and tracers from global ocean models.

#### Bottom:
- Interactions using bathymetry data (e.g., GEBCO or ETOPO1).

![ECCO Adjoint & State Estimation](pictures/overview-of-model.png)
**Fig: ECCO Adjoint & State Estimation (Credit NASA ECCO)**

### Key Concepts:
- **Forward Model:** Simulates changing conditions (e.g., ocean currents moving heat).
- **Data Differences:** Calculates the "misfit" between forward model output and observations.
- **Cost Function:** Measures how well model output matches observations.
- **Adjoint Model:** Adjusts control variables to reduce model-data differences.
- **Cost Function Gradient:** Provides directional information for iterative optimization.

## References:

Bates, N. R., Astor, Y. M., Church, M. J., Currie, K., Dore, J. E., González-Dávila, M., Lorenzoni, L., Muller-Karger, F., Olafsson, J., & Santana-Casiano, J. M. (2014). A time-series view of changing ocean chemistry due to ocean uptake of anthropogenic CO2 and ocean acidification. Oceanography, 27(1), 126–141. https://doi.org/10.5670/oceanog.2014.16

Bakker, D. C. E., Pfeil, B., Smith, K., Hankin, S., Olsen, A., Alin, S. R., Cosca, C., Harasawa, S., Kozyr, A., Nojiri, Y., O'Brien, K. M., Schuster, U., Telszewski, M., Tilbrook, B., Wada, C., Akl, J., Barbero, L., Bates, N. R., Boutin, J., Bozec, Y., Cai, W. J., Castle, R. D., Chavez, F. P., Chen, L., Chierici, M., Currie, K., de Baar, H. J. W., Evans, W., Feely, R. A., Fransson, A., Gao, Z., Hales, B., Hardman-Mountford, N. J., Hoppema, M., Huang, W. J., Hunt, C. W., Huss, B., Ichikawa, T., Johannessen, T., Jones, E. M., Jones, S. D., Jutterström, S., Kitidis, V., Körtzinger, A., Landschützer, P., Lauvset, S. K., Lefèvre, N., Manke, A. B., Mathis, J. T., Merlivat, L., Metzl, N., Murata, A., Newberger, T., Omar, A. M., Ono, T., Park, G. H., Paterson, K., Pierrot, D., Ríos, A. F., Sabine, C. L., Saito, S., Salisbury, J., Sarma, V. V. S. S., Schlitzer, R., Sieger, R., Skjelvan, I., Steinhoff, T., Sullivan, K. F., Sun, H., Sutton, A. J., Suzuki, T., Sweeney, C., Takahashi, T., Tjiputra, J., Tsurushima, N., van Heuven, S. M. A. C., Vandemark, D., Vlahos, P., Wallace, D. W. R., Wanninkhof, R., & Watson, A. J. (2014). An update to the Surface Ocean CO2 Atlas (SOCAT version 2). Earth System Science Data, 6(1), 69–90. https://doi.org/10.5194/essd-6-69-2014

DeVries, T. (2014). The oceanic anthropogenic CO2 sink: Storage, air-sea fluxes, and transports over the industrial era. Global Biogeochemical Cycles, 28, 631–647. https://doi.org/10.1002/2013GB004739

DeVries, T., Le Quéré, C., Andrews, O., Berthet, S., Hauck, J., Ilyina, T., Landschützer, P., Lenton, A., Lima, I. D., Nowicki, M., Schwinger, J., & Séférian, R. (2019). Decadal trends in the ocean carbon sink. Proceedings. National Academy of Sciences. United States of America, 116(24), 11,646–11,651. https://doi.org/10.1073/pnas.1900371116

Dore, J. E., Lukas, R., Sadler, D. W., Church, M. J., & Karl, D. M. (2009). Physical and biogeochemical modulation of ocean acidification in the central North Pacific. Proceedings. National Academy of Sciences. United States of America, 106(30), 12,235–12,240. https://doi.org/10.1073/pnas.0906044106

Feely, R. A., Takahashi, T., Wanninkhof, R., McPhaden, M. J., Cosca, C. E., Sutherland, S. C., & Carr, M. E. (2006). Decadal variability of the air-sea CO2 fluxes in the equatorial Pacific Ocean. Journal of Geophysical Research, 111, C08S90. https://doi.org/10.1029/2005JC003129

Landschützer, P., Gruber, N., Haumann, F. A., Rödenbeck, C., Bakker, D. C. E., van Heuven, S., Hoppema, M., Metzl, N., Sweeney, C., Takahashi, T., Tilbrook, B., & Wanninkhof, R. (2015). The reinvigoration of the Southern Ocean carbon sink. Science, 349(6253), 1221–1224. https://doi.org/10.1126/science.aab2620

Pfeil, B., Olsen, A., Bakker, D. C. E., Hankin, S., Koyuk, H., Kozyr, A., Malczyk, J., Manke, A., Metzl, N., Sabine, C. L., Akl, J., Alin, S. R., Bates, N., Bellerby, R. G. J., Borges, A., Boutin, J., Brown, P. J., Cai, W. J., Chavez, F. P., Chen, A., Cosca, C., Fassbender, A. J., Feely, R. A., González-Dávila, M., Goyet, C., Hales, B., Hardman-Mountford, N., Heinze, C., Hood, M., Hoppema, M., Hunt, C. W., Hydes, D., Ishii, M., Johannessen, T., Jones, S. D., Key, R. M., Körtzinger, A., Landschützer, P., Lauvset, S. K., Lefèvre, N., Lenton, A., Lourantou, A., Merlivat, L., Midorikawa, T., Mintrop, L., Miyazaki, C., Murata, A., Nakadate, A., Nakano, Y., Nakaoka, S., Nojiri, Y., Omar, A. M., Padin, X. A., Park, G. H., Paterson, K., Perez, F. F., Pierrot, D., Poisson, A., Ríos, A. F., Santana-Casiano, J. M., Salisbury, J., Sarma, V. V. S. S., Schlitzer, R., Schneider, B., Schuster, U., Sieger, R., Skjelvan, I., Steinhoff, T., Suzuki, T., Takahashi, T., Tedesco, K., Telszewski, M., Thomas, H., Tilbrook, B., Tjiputra, J., Vandemark, D., Veness, T., Wanninkhof, R., Watson, A. J., Weiss, R., Wong, C. S., & Yoshikawa-Inoue, H. (2013). A uniform, quality-controlled Surface Ocean CO2 Atlas (SOCAT). Earth System Science Data, 5(1), 125–143. https://doi.org/10.5194/essd-5-125-2013

Riebesell, U., Scholz, K. G., Bellerby, R. G. J., Botros, M., Fritsche, P., Meyerhö, M., Neill, C., Nondal, G., Oschlies, A., Wohlers, J., & Zöllner, E. (2007). Enhanced biological carbon consumption in a higher CO2 ocean. Nature, 450(7169), 545–548. https://doi.org/10.1038/nature06267

