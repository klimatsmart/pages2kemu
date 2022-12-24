## PAGES 2k tree ring chronology calculations

How to reproduce some noteworthy tree ring chronologies from the PAGES 2k network, using the programs ARSTAN and RCSsigFree on Linux. See Climate Audit post for context: https://climateaudit.org/2021/08/15/pages19-asian-tree-ring-chronologies/

### Download and compile ARSTAN

1. Download source code: https://www.ldeo.columbia.edu/res/fac/trl/public/ftp/Kevin/ARSTAN_Intel.zip
2. Extract the file ARSTAN_Intel/Archive/ARSTAN41b_OSX.f.
3. Delete the contents of the subroutines crnplt1, crnplt3, crnplt5, crnplt7, crnplt11, power1, loads1, scores1 and arhist1.
4. Compile with GNU Fortran (tested with version 9.4.0): gfortran -o ARSTAN41b_OSX ARSTAN41b_OSX.f -ffixed-line-length-none

### Download and compile RCSsigFree

1. Download source code: https://www.ldeo.columbia.edu/res/fac/trl/public/ftp/pjk/Baji/RCS_SgnFree_AWE.zip
2. Extract the file RCS_SgnFree_AWE/archive/archive/NewNov_2011/SignalFree_Median.f.
3. Delete the contents of the subroutines plot1 and spaghetti.
4. Replace dabs with abs in lines 1230, 1232 and 1235.
5. Compile with GNU Fortran: gfortran -o SignalFree_Median SignalFree_Median.f -ffixed-line-length-none

### Example 1: Reproduce the paki033 chronology using RCSsigFree

1. Download measurement data: https://www.ncei.noaa.gov/pub/data/paleo/treering/measurements/asia/paki033.rwl
2. Run SignalFree_Median with input file paki033.rwl.
3. Use all data series and otherwise the settings indicated in the log file RCS_SgnFree_AWE/archive/archive/NewNov_2011/"SignalFree_Median2 output".

The last column in the output file paki033_crns_col.txt should be identical to the PAGES 2k chronology available here: https://www.ncei.noaa.gov/pub/data/paleo/pages2k/pages2k-temperature-v2-2017/data-current-version/Asi-PAKI033.Cook.2013.txt

The second to last column is the corresponding chronology without signal-free iterations.

### Example 2: Reproduce the paki036 chronology using ARSTAN and RCSsigFree

1. Download measurement data: https://www.ncei.noaa.gov/pub/data/paleo/treering/measurements/asia/paki036.rwl
2. Pass paki036.rwl through ARSTAN41b_OSX to fill in missing values. Set option "core series save" to save series in Tucson raw data format.
3. Run SignalFree_Median with input file paki036.rwl_gap and the same settings as before.

The last column in the output file paki036_crns_col.txt should be identical to the PAGES 2k chronology available here: https://www.ncei.noaa.gov/pub/data/paleo/pages2k/pages2k-temperature-v2-2017/data-current-version/Asi-PAKI036.Cook.2013.txt
