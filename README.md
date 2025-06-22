# cspqaes
Preparing compressing sensing over matlab and pqaes over python to be modulated with hackrf
* Downloading the image
```
sudo su
```
```
docker image pull ubuntu:18.04
```
```
docker images
```
OR
```
docker image ls
```
change name_session with realusername , for me it's dast, use this [link](https://stackoverflow.com/questions/3522341/identify-user-in-a-bash-script-called-by-sudo)
```
docker run -itd --privileged --cap-add=ALL -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro -v /media/$SUDO_USER/:/media:ro --net=host --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8"  --name  cspqaes ubuntu:18.04
```
```
docker restart cspqaes
```
```
xhost +
```
```
docker exec -ti cspqaes bash
```
```
apt update
```
```
apt install ubuntu-desktop wget nano zip
```
* Installing Hackrf drivers
```
apt install hackrf gnuradio rtl-sdr ffmpeg vlc gr-osmosdr
```
```
apt install git unzip
```
```
hackrf_info
```
```
apt update
```
```
apt-get install python3-pip wget
```
```
apt-get install python3-pip
```
```
pip3 install progressbar
```
```
pip3 uninstall numpy
```
```
pip3 install "numpy<1.20.0"
```
```
apt install python3-distutils
```
```
pip3 install "click>7.1.0"
```
```
pip3 show click
```
```
pip3 install progress
```
```
pip3 install sympy
```
```
pip3 install Exit
```
```
apt install -y dh-python python3-click python3-progress  python3-numpy python3-matplotlib python3-networkx   python3-stdeb python3-setuptools-scm python3-setuptools python3-cpuinfo
```
```
pip3 install dh click numpy progress matplotlib networkx stdeb setuptools-scm setuptools
```
```
apt-get install python-all
```
```
mkdir isogenies
```
```
cd isogenies
```
```
git clone https://github.com/Krijn-math/Constant-time-CSURF-CRADS
```
```
cd Constant-time-CSURF-CRADS/
```
```
python3 main.py --help
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd1 -v -a csidh -e 10
```
```
python3 main.py -p p512  -m scaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csurf -e 5
```
```
cd ..
```

* Installing sibc 
```
git clone https://github.com/JJChiDguez/sibc
```
```
cd sibc
```
Open setup.py by nano
```
nano setup.py
```
search long_description and change : </br>
```
with open("README.md", "r") as obj : 
```
by
```
with open("README.md", "r", encoding="utf-8") as obj : 
```
```
python3 setup.py bdist_deb
```
```
python3 setup.py install
```
Tape before benchmark csidh
```
export LC_ALL=C.UTF-8
```
```
export LANG=C.UTF-8
```
```
python3 sibc csidh-bench
```
```
python3 sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
```
sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
```
cd ..
```
* TESTING CRYPTODOME
Testing :
```
mkdir cryptodome
```
```
cd cryptodome
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/real_csidh.py
```
```
python3 real_csidh.py 
```
Launching separate mode for csidh sibc
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/keygen_csidh_sibc.py
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/shared_csidh_sibc.py
```
```
rm -rf *.pub *.priv *.key
```
```
python3 keygen_csidh_sibc.py -n alice
```
```
ls
```
```
python3 keygen_csidh_sibc.py -n bob
```
```
ls
```
```
python3 shared_csidh_sibc.py -p alice.pub -s bob.priv -k key1.key
```
```
python3 shared_csidh_sibc.py -p bob.pub -s alice.priv -k key2.key
```
* FO-PQAES
```
git clone https://github.com/SitrakaResearchAndPOC/Python_PQAES_FO.git
```
```
cd Python_PQAES_FO/
```
```
unzip Python-PQAES.zip 
```
```
cd Python-PQAES-CSIDH/
```
key in hexadecimal : 
```
python3 AES.py -e test.txt -c 128
```
```
python3 AES.py -d test.txt.aes -c 128
```
Name the decrypted file as test_dec.txt
```
tail -f test_dec.txt
```
```
python3 FO.py 
```
```
python3 FO.py -e test.txt -a sha256 -k bob.priv 
```
```
python3 FO.py -d test.txt.fo -a sha256 -k bob.priv 
```
```
tail -f test_fo.txt
```
* CHECK PQAES
```
python3 PQAES.py
```
```
cd ../../..
```


* Installing [ECLIPSE](https://www.tecmint.com/eclipse-install-ubuntu/) or [ECLIPSE2](https://www.makeuseof.com/install-eclipse-ide-on-linux/)
```
cd /
```
```
apt install default-jre
```
```
wget http://ftp.yz.yamagata-u.ac.jp/pub/eclipse/oomph/epp/2023-06/R/eclipse-inst-jre-linux64.tar.gz
```
```
tar -xvf eclipse-inst-jre-linux64.tar.gz
```
```
cd eclipse-installer/
```
```
./eclipse-inst
```
Select "eclipse IDE for java developpers" </br>
Choose one options of jdk and click to install, should be take a little bit time </br> </br> 
If problem, find the real name of java install directory : ls /root/eclipse/java-2023-06
```
cd /root/eclipse/java-2023-06/eclipse/
```
```
./eclipse
```
Create new project in default workspace and create ClassMain with System.out.println("hello world"); for testing </br> </br>
create bash scripting
```
nano eclipse.sh
```
copy the script bash and save on eclipse.sh 
```
#!/bin/sh
echo "launching eclipse"
cd /root/eclipse/java-2023-06/eclipse/
./eclipse
```
```
chmod +x eclipse.sh
```
```
exit
```
```
xhost +
```
```
docker exec -ti cspqaes bash eclipse.sh
```

* INSTALLING MATLAB 2018
```
mkdir MATLAB
```
```
cd MATLAB
```
```
mkdir INSTALL
```
open the two file using diskimager : </br>
utf-8''r2018b_glnxa64_dvd1.iso </br>
utf-8''r2018b_glnxa64_dvd2.iso </br>
</br>
Mounting point is : /media/name_session/name_dvd </br>
for me : name_session it's dast et name_dvd are MATHWORKS_R2018B et MATHWORKS_R2018B1 </br>
```
cp -rf /media/MATHWORKS_R2018B/* INSTALL
```
```
cp -rf /media/MATHWORKS_R2018B1/* INSTALL
```
```
cd INSTALL
```
```
bash install
```
Enter the right key : </br>
For me , it's : 
```
09806-07443-53955-64350-21751-41297
```
```
1) standalone:
- Install choosing the option "Use a File Installation Key" and supply the following FIK
	09806-07443-53955-64350-21751-41297
- To install Matlab Production Server,using this
	40236-45817-26714-51426-39281
- Use license_standalone.lic to activate,
  or copy license_standalone.lic to %installdir%\licenses\ ,and run matlab without activation
- after the installation finishes copy the folders to %installdir% to overwriting the originally installed files

2) floating license (network license server):
- Install choosing the option "Use a File Installation Key" and supply the following FIK
	31095-30030-55416-47440-21946-54205
- To install Matlab Production Server,using this
	57726-51709-20682-42954-31195
- Use license_server.lic when asked
- after the installation finishes copy the folders to %installdir% to overwriting the originally installed files
```
INSTALLATION FILE IS IN : /usr/local/MATLAB/R2018b </br>
use this command for changing path : 
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/MATLAB_R2018b_Linux64_Crack/main/MATLAB_R2018b_Linux64_Crack.zip
```
```
unzip MATLAB_R2018b_Linux64_Crack.zip
```
```
mv 'MATLAB R2018b Linux64 Crack' MATLABLIC
```
```
cp MATLABLIC/license_standalone.lic /usr/local/MATLAB/R2018b/bin/
```
```
cp -rf  MATLABLIC/R2018b/bin/glnxa64/* /usr/local/MATLAB/R2018b/bin/glnxa64/
```
```
cd /usr/local/MATLAB/R2018b/bin/
```
```
./matlab
```
Find the certificate at /usr/local/MATLAB/R2018b/bin/ as license_standalone.lic </br>
create bash scripting for matlab
```
exit 
```
```
xhost +
```
```
docker exec -ti cspqaes bash
```
```
cd /
```
```
nano matlab.sh
```
create and save 
```
#!/bin/sh
echo "launching matlab 2018"
cd /usr/local/MATLAB/R2018b/bin/
./matlab
```
```
chmod +x matlab.sh
```
```
exit 
```
```
xhost +
```
```
docker exec -ti cspqaes bash matlab.sh
```
If problem displaying plot exist, restart docker : 
```
exit 
```
```
docker restart cspqaes 
```
* saving images if you need
```
docker commit cspqaes  cspqaes:v1 
```
* IMAGE CS-PQAES v1 (DIFF BETWEEN LINUX AND WINDOWS)

Look at diff file </br>
MODIFICATION 1 : partie_1.m
```
diff -ru "matlabCS_Linux/partie_1.m" matlabCS_Windows/partie_1.m
--- "matlabCS_Linux/partie_1.m"	2024-07-21 14:26:16.000000000 +0300
+++ matlabCS_Windows/partie_1.m	2024-08-11 15:37:34.000000000 +0300
@@ -1,12 +1,12 @@
 %% function simulation_cs()
 %% INPUT VARIABLES FOR JAVA:
 %% Ciphering parameters:
-binPath     = 'D:\ECLIPSE_PROJECT\Article4_QuantumCipherMode2\bin';
-cipherClass = 'main_pkg.Main';
+binPath     = '/root/eclipse-workspace/Article4_QuantumCipherMode2/bin';
+cipherClass = 'main_pkg.Cipher';
 cipherModes = {'AES','PQAES_SHA','PQAES_SHA3','PQAES_KECCAK','PQAES_SHAKE'};
 cipherMode  = cipherModes{1};
-compressed_image_path = 'C:\Users\Sitraka\Documents\MATLAB\matlabCS_Linux\input_java';
-ciphered_image_path   = 'C:\Users\Sitraka\Documents\MATLAB\matlabCS_Linux\output_java';
+compressed_image_path = '/usr/local/MATLAB/R2018b/bin/matlabCS_Windows/input_java';
+ciphered_image_path   = '/usr/local/MATLAB/R2018b/bin/matlabCS_Windows/output_java';
 
 %% 1- GET THE IMAGE
@@ -67,12 +67,14 @@
 %% Write the image in the file input Java:
 input_image_name = 'image.csv';
 parent           = cd(compressed_image_path);
-writematrix(image,input_image_name);
+dlmwrite(input_image_name, image);
 cd(parent);
  
  inputImagePath      = appendToPath(compressed_image_path,input_image_name);
- inputImagePath      = normalizePathForJava(inputImagePath);
- outputs_java        = normalizePathForJava(ciphered_image_path);
+ %inputImagePath      = normalizePathForJava(inputImagePath);
+%outputs_java        = normalizePathForJava(ciphered_image_path);
+outputs_java        = ciphered_image_path;
+
 %% JAVA PART:
 % javaCipheringLauncher(binPath,className,cipherType,input_path,output_path,ligne,colonne)
 javaCipheringLauncher(binPath,cipherClass,cipherMode,inputImagePath,outputs_java,ligne_cr,colonne);
@@ -80,7 +82,7 @@
 %% READ CIPHERED IMAGE OUTPUT BY JAVA: 
 imageCipheredPath = appendToPath(ciphered_image_path,'imageCiphered');
 parent = cd(imageCipheredPath);
-image = readmatrix('imageCiphered.csv');
+image = dlmread('imageCiphered.csv');
 cd(parent);
 
 %% Steganography instertion:
@@ -93,23 +95,26 @@
 image = istega(image_stego);
 image = round(image);
 %% Path Variables for imageDeCiphering
-imageToDecipherPath = 'C:\Users\Sitraka\Documents\MATLAB\matlabCS_Linux\imageToDecipher';
+imageToDecipherPath = '/usr/local/MATLAB/R2018b/bin/matlabCS_Windows/imageToDecipher/';
 parent =cd(imageToDecipherPath);
-writematrix(image,'imageToDecipher.csv');
+dlmwrite('imageToDecipher.csv', image);
 cd(parent)
 
 %% Partie 2 Java:
 %% PARAMETERS:
-binPath = 'D:\ECLIPSE_PROJECT\Article4_QuantumCipherMode2\bin';
+binPath = '/root/eclipse-workspace/Article4_QuantumCipherMode2/bin';
 decipherClass = 'main_pkg.DeCipher';
 cipheringType = cipherModes{1};
-parametersPath = normalizePathForJava(ciphered_image_path);
-imageToDecipherPath = normalizePathForJava(appendToPath(imageToDecipherPath,'imageToDecipher.csv'));
+%parametersPath = normalizePathForJava(ciphered_image_path);
+parametersPath = ciphered_image_path;
+% imageToDecipherPath = normalizePathForJava(appendToPath(imageToDecipherPath,'imageToDecipher.csv'));
+imageToDecipherPath = appendToPath(imageToDecipherPath,'imageToDecipher.csv');
+
 javaDecipheringLauncher(binPath,decipherClass,cipheringType,parametersPath,imageToDecipherPath,ligne_cr,colonne)
 %% -----------------------------------------------------------------------------------------------------%%
 %% READ FINAL OUTPUT
-parent = cd('C:\Users\Sitraka\Documents\MATLAB\matlabCS_Linux\output_java\finalOutput');
-image = readmatrix('finalOutput.csv');
+parent = cd('/usr/local/MATLAB/R2018b/bin/matlabCS_Windows/output_java/finalOutput');
+image = dlmread('finalOutput.csv');
Only in matlabCS_Windows: test.txt
```
MODIFICATION 2 : javaLauncher*.m

For finding eclise commande : </br>
In RUN / RUN CONFIGURATIONS... / SHOW COMMAND LINE (in eclpise) </br>
Full command java should be replaced as sprintf on MATLAB code 
```
diff -ru "matlabCS_Linux/javaCipheringLauncher.m" matlabCS_Windows/javaCipheringLauncher.m
--- "matlabCS_Linux/javaCipheringLauncher.m"	2024-07-21 09:42:08.000000000 +0300
+++ matlabCS_Windows/javaCipheringLauncher.m	2024-08-11 14:57:51.000000000 +0300
@@ -1,6 +1,6 @@
 function javaCipheringLauncher(binPath,className,cipherType,input_path,output_path,ligne,colonne)
 %% PARAMETERS TO CHANGE: 
-    command = sprintf('java -cp %s %s %s %s %s %d %d',binPath, className,cipherType,input_path,output_path,ligne,colonne);
+    command = sprintf('/root/.p2/pool/plugins/org.eclipse.justj.openjdk.hotspot.jre.full.linux.x86_64_17.0.11.v20240426-1830/jre/bin/java -cp %s %s %s %s %s %d %d',binPath, className,cipherType,input_path,output_path,ligne,colonne);
     [~,s] = system(command);
     disp(s)
 end
diff -ru "matlabCS_Linux/javaDecipheringLauncher.m" matlabCS_Windows/javaDecipheringLauncher.m
--- "matlabCS_Linux/javaDecipheringLauncher.m"	2024-07-21 10:29:34.000000000 +0300
+++ matlabCS_Windows/javaDecipheringLauncher.m	2024-08-11 14:58:09.000000000 +0300
@@ -7,6 +7,6 @@
 % ligne = 192;
 % colonne = 256;
 
-command = sprintf('java -cp %s %s %s %s %s %d %d',binPath, decipherClass,cipheringType,parametersPath,imToDecipherPath,ligne,colonne);
+command = sprintf('/root/.p2/pool/plugins/org.eclipse.justj.openjdk.hotspot.jre.full.linux.x86_64_17.0.11.v20240426-1830/jre/bin/java -cp %s %s %s %s %s %d %d',binPath, decipherClass,cipheringType,parametersPath,imToDecipherPath,ligne,colonne);
 [r,s] = system(command);
 disp(s)
\ No newline at end of file
Only in matlabCS_Windows: myFile.txt
```




* BONUS , INSTALLING ECLIPSE ON REAL MACHINE NOT DOCKER
[snapd](https://forum.snapcraft.io/t/system-does-not-fully-support-snapd/14767  and reboot)
```
apt install fuse squashfuse
```
```
apt install snapd
```
```
snap refresh
```
#snap install eclipse --classic
```
snap install --classic eclipse
```
others ideas,
```
Open /Users/{Your_Dir_Name}/.eclipse; right click on .eclipse,then change permission read-only to read and w.
snap reflesh
snap install --classic eclipse
```


* LINKS

```
ubuntu-drivers devices
```

[driver_info](https://medium.com/@supermellow.ai/how-to-install-graphic-card-driver-in-ubuntu-22-04-c9e4c0a8f00b)
