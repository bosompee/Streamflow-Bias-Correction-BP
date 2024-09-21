The USGS NHM-PRMS streamflow results (Hay, 2019) were downloaded from the USGS ScienceBase (Application of the National Hydrologic Model Infrastructure with the Precipitation-Runoff Modeling System (NHM-PRMS), by HRU Calibrated Version - ScienceBase-Catalog). Here is the link to the USGS website where you can download streamflow and the other outputs; https://www.sciencebase.gov/catalog/item/5a4ea3bee4b0d05ee8c6647b. An explanation of the files for the NHM streamflow download are:

1)	Carb Project to share.ppkx – this is an ArcMap project where the CARB segment outflows (stream discharge) for each segment can be visualized. Note that t_1 is October 1, 1980, and t_2 is October 2, 1980 etc..
2)	CARB_segments_final.csv – this is a list of the segment numbers that are included in CARB. This provides information about which segment numbers in our region that we want to output.
3)	CARBSegments Final.R – this is the R code that will go through netCDF file and pull out all the data relevant to our site.
4)	CARBstreamflow_final_v2!.csv – this is the output of #3, so a giant CSV file that has all the stream outflows for each of the segments in our region. What was done in #1 is connect those segment locations back to their physical location in ArcMap. The geospatial fabric data can be found here (https://www.sciencebase.gov/catalog/item/535eda80e4b08e65d60fc834). We used ArcMap to bring in the segment distributions and clip to our region, then exported the segment IDs for use in #3.
5)	Seg_outflow.nc – the giant netCDF file from Will with all the stream segment outflows for the nation. This is used in #3 to go through and pull out those associated with #2 to create #4.
 
The USGS measured streamflow results were obtained from the National Water Information System (NWIS) (USGS, 2022) (Water Resources of the United States—National Water Information System (NWIS) Mapper (usgs.gov), for example: (USGS 07130500 ARKANSAS RIVER BELOW JOHN MARTIN RESERVOIR, CO.). The code used to download the measured streamflow is in the R file "DATA DOWLOAD_USGS GAGES". The stream gages for our region is compiled in the "newSteamGagesCARB_2a" csv file and get a vector of all the gages and put in the vectors to download the specific gages.
 
## STEPS FOR THE BIAS CORRECTION
1. Comparing simulated NHM streamflow to observed/measured streamflows revealed considerable mismatch. This analysis was carried out for all the gages in the CARB but R file "SimMeasuredCombined" shows the analysis for gages A, B, C and D.
2. Flow Duration Curves (FDC) was carried out on all the gages where a volume of the NHM simulated streamflow and probability at a point was mapped to the same probability on the measured streamflow and the corresponding streamflow value was used as the bias corrected FDC simulated streamflow at that point (Bum Kim et al., 2021; Farmer et al., 2018). This analysis was carried out for all the gages in the CARB but R file "CombinedMethodsTS_all_BCmethods" shows the FDC analysis for gages A, B, C and D.
3. Autoregressive Integrated Moving Average (ARIMA) were constructed from a time series of the residuals calculated from the observed and NHM-PRMS simulated streamflow. This analysis was carried out in 3 steps ie. Identification, Estimation and Diagonistic checking or validation. The code for this analysis can also be found in "CombinedMethodsTS_all_BCmethods".
4. The Train and Test code for FDC and ARIMA to determine the predictive ability of methods can be found in the R files "FDC_train_test", "ARIMA_train_test_CombinedTS" and "FDC_ARIMA_train_test". NB: Some of the analysis was carried out in Rmarkdown (RMD).
5. Forecasting was carried out on the ARIMA using the Rmarkdown file "Forecast" for all the gages in the CARB.

