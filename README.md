***To setup the code, please, follow:***

ssh -XY username@lxplus8.cern.ch

voms-proxy-init -voms cms

cmsrel CMSSW_14_1_3

cd CMSSW_14_1_3/src

cmsenv

git clone -b 14_1_3 git@github.com:RAGHUMATAPITA/2024HIRunNtupleTest.git .

scram b -j 8

To prepare the trees and histograms for performance plots, please, use:

HITrackingStudies/HITrackingStudies/test/run_PbPb_cfg.py

For control plots, see macros:

HITrackingStudies/HITrackingStudies/test/plottingMacro/macro_control_plots_XXX.C

For efficiency and fake rate use:

HITrackingStudies/HITrackingStudies/test/plottingMacro/plotHistXXX.C

***Making performance tree***
navigate to the analyzer directory:

cd HITrackingStudies/test/

edit run_PbPb_cfg.py to get the settings you want (the cuts are the most relevant thing here)

One example:

cmsRun run_PbPb_cfg.py sample="Data_MiniAOD" n=100 usePixelTrks=False runOverStreams=False >& OutPut.txt &

***For doing control plots run***

Somehow, these macro are not working in CMSSW_14_1_X. 

One can run this macro in CMSSW_13_X_X. You can use CMSSW_13_2_10 or 13_2_5_pacth1.

Use the output file produced from cmsRun as input file to the following macro which can be found inside HITrackingStudies/HITrackingStudies/test/plottingMacro

root -l -b -q macro_control_plots_OneSample.C

root -l -b -q macro_control_plots_TwoSamples.C

root -l -b -q macro_control_plots_ThreeSamples.C

root -l -b -q macro_control_plots_signal_vs_fake_MCrecodebugOnly.C // Only for RECODEBUG sample

***Plotting efficiency/fake***
Use the output file produced from cmsRun as input file

In the 'plottingMacro' directory from the above path:

root -l -b -q plotHist2D.C

Output plots will be in the 'files' directory. And TGraphs in "test.root" file

