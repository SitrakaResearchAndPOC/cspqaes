* RESUME OF DIFF BETWEEN LINUX AND WINDOWS matlabCS 
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
MODIFICATION 2 : java*Launcher.m

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
