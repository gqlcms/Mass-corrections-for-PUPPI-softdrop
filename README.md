# Mass-corrections-for-PUPPI-softdrop
```
float puppiCorr = getPUPPIweight( AK8jetPt , AK8jetEta );
float jetmass = AK8PUPPISoftdropUncorrectedMass*puppiCorr;

float ExoDiBosonAnalysis::getPUPPIweight(float puppipt, float puppieta ){

 TFile* file = TFile::Open( "weights/puppiCorr_2017.root","READ");
  puppisd_corrGEN      = (TF1*)file->Get("puppiJECcorr_gen");
  puppisd_corrRECO_cen = (TF1*)file->Get("puppiJECcorr_reco_0eta1v3");
  puppisd_corrRECO_for = (TF1*)file->Get("puppiJECcorr_reco_1v3eta2v5");


  float genCorr  = 1.;
  float recoCorr = 1.;
  float totalWeight = 1.;
        
  genCorr =  puppisd_corrGEN->Eval( puppipt );
  if( fabs(puppieta)  <= 1.3 ){
    recoCorr = puppisd_corrRECO_cen->Eval( puppipt );
  }
  else{
    recoCorr = puppisd_corrRECO_for->Eval( puppipt );
  }
  
  totalWeight = genCorr * recoCorr;

  return totalWeight;
}
```
