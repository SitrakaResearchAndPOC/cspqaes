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
```
docker rm -f cspqaes
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
Verify if the number of the directory on container is more less than ubuntu desktop
```
dir
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
apt install python3-pip wget
```
```
apt install python3-pip
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
apt install python-all
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
ls alice*
```
```
python3 keygen_csidh_sibc.py -n bob
```
```
ls bob*
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

</br>
The file "test.txt" already exists. Overwrite? [y/n] </br>
Tape n </br>
The name of decrypted file as `test_dec.txt` </br>
</br>

```
tail -f test_dec.txt
```

Tape ctrl+C to break the console terminal

```
python3 FO.py 
```
```
python3 FO.py -e test.txt -a sha256 -k bob.priv 
```
```
python3 FO.py -d test.txt.fo -a sha256 -k bob.priv 
```

</br>
The file "test.txt" already exists. Overwrite? [y/n] </br>
Tape  n </br>
The name of decrypted file as `test_fo.txt` </br>
</br>

```
tail -f test_fo.txt
```

Tape ctrl+C to break the console terminal


* CHECK PQAES
```
python3 PQAES.py
```
```
cd ../../../..
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
cd /
```
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
cp eclipse.sh /root/eclipse/java-2023-06/eclipse/
```
```
cp eclipse.sh root/eclipse-workspace/
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
xhost +
```
```
docker exec -ti cspqaes bash 
```

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
exit
```
```
docker stop cspqaes
```
```
docker start cspqaes
```
```
xhost +
```
```
docker exec -ti cspqaes bash 
```
```
cd MATLAB
```

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
Use installation for key </br>
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
cp matlab.sh /usr/local/MATLAB/R2018b/bin/
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
Removing installer source for matlab
```
docker exec -ti cspqaes bash
```
```
rm -rf MATLAB
```
If problem displaying plot exist, restart docker : 
```
exit 
```
```
xhost +
```
```
docker restart cspqaes 
```
* Cleaning CSPQAES code :
```
cd /root/eclipse-workspace/
```
```
rm -rf *
```
```
cd /usr/local/MATLAB/R2018b/bin/
```
```
dir
```
```
rm -rf matlabCS*
```

* Insertion of code version matlabCS_v1 (the compressive sensing is not so performed)
```
cd /root/eclipse-workspace/
```
Inspired at [quantum_cipher](https://raw.githubusercontent.com/Safidiko/AES-PQAES/main/Article4_QuantumCipherMode2.zip) the main.java should be renamed as Cipher.java for having the version on [my_repo](https://raw.githubusercontent.com/SitrakaResearchAndPOC/cspqaes/refs/heads/main/PostQuantumCryptography/Article4_QuantumCipherMode2.zip)
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/cspqaes/refs/heads/main/PostQuantumCryptography/Article4_QuantumCipherMode2.zip
```
```
unzip Article4_QuantumCipherMode2.zip
```
Launch eclipse
```
bash /eclipse.sh
```
Import eclipse project</br></br>
FILE / IMPORT / GENERAL / EXISTING PROJECT INTO WORKSPACE / BROWSE / SELECT Article4_QuantumCipherMode2  / OPEN </br> </br>
RUN TO JAVA CODE at /Article4_QuantumCipherMode2/src/main_pkg/ : Cipher.java and Decipher.java </br>
IF ANY PROBLEM WHEN LAUNCHING Cipher.java & Dechipher.java : INSERT ALSO IN RUN : RUN / RUN CONFIGURATIONS / JAVA APPLICATION / MAIN / ADD PROJECT --> so add Article4_QuantumCipherMode2 </br> </br>

For finding eclipse commande : </br>
In RUN / RUN CONFIGURATIONS/JAVA APPLICATION/ ARGUMENTS / SHOW COMMAND LINE (maybe need to run the mainclass in eclpise) </br></br>
COPY LONGUE JAVA COMMAND IN TXT DOCUMENT Something Like  :  </br>
/root/.p2/pool/plugins/org.eclipse.justj.openjdk.hotspot.jre.full.linux.x86_64_17.0.15.v20250423-0846/jre/bin/java </br>
OR USE COMMAND : find ~/.p2 -type f -name java
</br>
Exit all eclipse GUI </br>
```
cd /usr/local/MATLAB/R2018b/bin/
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/cspqaes/refs/heads/main/CS_v1/matlabCS_Linux.zip
```
```
unzip matlabCS_Linux.zip
```
```
cd matlabCS_Linux
```
```
nano javaCipheringLauncher.m
```
Full command java should be replaced as sprintf on MATLAB code by PASTING LONGUE JAVA COMMAND IN TXT DOCUMENT 
```
nano javaDecipheringLauncher.m
```
Full command java should be replaced as sprintf on MATLAB code by PASTING LONGUE JAVA COMMAND IN TXT DOCUMENT 
```
bash /matlab.sh
```
Go to matlabCS_Linux/partie_1.m </br>
Launch partie_1.m</br>
Exit all GUI</br>

* Insertion of code version matlabCS_v2 (good performance of compressive sensing)
Launch eclipse
```
bash /eclipse.sh
```
Import eclipse project</br></br>
FILE / IMPORT / GENERAL / EXISTING PROJECT INTO WORKSPACE / BROWSE / SELECT Article4_QuantumCipherMode2  / OPEN
INSERT ALSO IN RUN : RUN / RUN CONFIGURATIONS / JAVA APPLICATION / MAIN / ADD PROJECT --> so add Article4_QuantumCipherMode2
</br>


Exit all eclipse GUI </br>
```
cd /usr/local/MATLAB/R2018b/bin/
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/cspqaes/refs/heads/main/CS_v2/matlabCS2_Linux2.zip
```
```
unzip matlabCS2_Linux2.zip
```
COPY THE OUTPUT
```
find ~/.p2 -type f -name java
```
```
nano javaCipheringLauncher.m
```
Full command java should be replaced as sprintf on MATLAB code by PASTING LONGUE JAVA COMMAND COPYING BEFORE </br>
Tape ctrl+x  and yes for saving
COPY THE OUTPUT
```
find ~/.p2 -type f -name java
```
```
nano javaDecipheringLauncher.m
```
Full command java should be replaced as sprintf on MATLAB code by PASTING LONGUE JAVA COMMAND COPYING BEFORE </br>
Tape ctrl+x  and yes for saving
```
bash /matlab.sh
```

Select matlabCS2_Linux2 </br>
Open bloc_emission.m and bloc_reception.m </br>
</br>
Run bloc_emission.m </br>
```
cd /usr/local/MATLAB/R2018b/bin/matlabCS2_Linux/Resultat_Emission
```
```
xdg-open <image>
```
Run bloc_reception.m </br>
```
cd /usr/local/MATLAB/R2018b/bin/matlabCS2_Linux/Resultat_Reception
```
```
xdg-open <image>
```



* saving images if you need
```
docker commit cspqaes  cspqaes:v1 
```


* LINKS

```
ubuntu-drivers devices
```

[driver_info](https://medium.com/@supermellow.ai/how-to-install-graphic-card-driver-in-ubuntu-22-04-c9e4c0a8f00b)
