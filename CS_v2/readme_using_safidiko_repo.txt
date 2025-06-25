cd /usr/local/MATLAB/R2018b/bin
wget https://github.com/Safidiko/matlabCS2/raw/refs/heads/main/matlabCS2.zip
unzip matlabCS2.zip

cp -r matlabCS2 matlabCS2_Linux
cp -r matlabCS2 matlabCS2_Windows


modify : matlabCS2_Linux
cd /
bash matlab.sh

**************


Lancer bloc_emission.m

Fermer 


utiliser mode real : 

cd /usr/local/MATLAB/R2018b/bin/matlabCS2_Linux/Resultat_Emission
xdg-open <image>

cd /
bash matlab.sh


lancer bloc_reception


fermer : 

cd /usr/local/MATLAB/R2018b/bin/matlabCS2_Linux/Resultat_Reception
xdg-open <image>



original image : 
cd /usr/local/MATLAB/R2018b/bin/matlabCS2_Linux/Resultat_Reception
xdg-open <image> 

zip -r matlabCS2_Linux.zip matlabCS2_Linux
zip -r matlabCS2_Windows.zip matlabCS2_Windows

exit


mkdir old_vesion

docker cp cspqaes:/usr/local/MATLAB/R2018b/bin/matlabCS2_Linux.zip .
docker cp cspqaes:/usr/local/MATLAB/R2018b/bin/matlabCS2_Windows.zip .

cd ..

mkdir old_version2
cd old_version2


Pour mode simulated : 
ouvrir tous les fichiers : imageComparator.mlapp, histogramApp.mlapp, imageView.mlapp puis fermer 
Puis clic droit/open/select code view instead design view et cliquer sur run

zip -r matlabCS2_Linux2.zip matlabCS2_Linux
zip -r matlabCS2_Windows2.zip matlabCS2_Windows

exit
docker cp cspqaes:/usr/local/MATLAB/R2018b/bin/matlabCS2_Linux2.zip .
docker cp cspqaes:/usr/local/MATLAB/R2018b/bin/matlabCS2_Windows2.zip .

cd ..

copier les fichiers  imageComparator de chaque dans un dossier en nommant imageComparator_mandeha.mlapp pour oldversion1 et  imageComparator_tsymandeha.mlapp pour oldversion2
unzip imageComparator_ok.mlapp -d imageComparator_ok
unzip imageComparator_not_ok.mlapp -d imageComparator_not_ok
diff -ru imageComparator_ok imageComparator_not_ok > imageComparator.diff


