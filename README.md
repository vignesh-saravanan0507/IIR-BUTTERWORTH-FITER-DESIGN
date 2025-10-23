# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
~~~
clc ; 
close ; 
wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
 
//Pre warping- Bilinear Transformation 
omegap=(2/T)*tan(wp/2); 
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas='); 
 
//Order of the filter 
 
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap)); 
disp(N,'N='); 
13 
 
N=ceil(N); 
 
disp(N,'Round off value of N='); 
 
 
//Cut off frequency 
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N))); 
disp(omegac,'omegac='); 
 
disp('Normalised Analog LPF Transfer function H(S)='); 
hs_Normalised = analpf(N,'butt',[0,0],1); 
disp(hs_Normalised); 
 
disp('Analog LPF Transfer function H(S)='); 
hs= analpf(N,'butt',[0,0],omegac); 
disp(hs); 
 
 
z=poly(0,'z');//Defining variable z 
 
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation 
disp('Digital LPF Transfer function H(Z)='); 
disp(Hz); 
 
 
HW=frmag(Hz,512); // Frequency response 
w=0:%pi/511:%pi ; 
plot(w/%pi,abs(HW)); 
 
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude '); 

 
title(' Frequency Response of Butterworth IIR LPF');
~~~

## PROGRAM (HPF): 
~~~
clc;
close;
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)= ');
alphas = input('Enter the stop band attenuation (dB)= ');
T = input('Enter the Value of sampling Time= ');

// Pre-warping (Bilinear Transformation)
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1)) / (2*log10(omegas/omegap));
disp(N,'N=');
N = ceil(N);
disp(N,'Round off value of N=');

// Cut off frequency
omegac = omegap / (((10^(0.1*alphap))-1)^(1/(2*N)));
disp(omegac,'omegac=');

// Normalised Analog LPF Transfer function
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);

// Analog LPF Transfer function
disp('Analog LPF Transfer function H(S)=');
hs = analpf(N,'butt',[0,0],omegac);
disp(hs);

s = poly(0,'s');
hpf_s = horner(hs, omegac/s);   // substitute s → omegac/s
disp('Analog HPF Transfer function H(S)=');
disp(hpf_s);

// Bilinear Transformation to Digital
z = poly(0,'z'); // Defining variable z
Hz = horner(hpf_s,(2/T)*((z-1)/(z+1))); 
disp('Digital HPF Transfer function H(Z)=');
disp(Hz);

// Frequency Response
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(HW));

xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude');
title(' Frequency Response of Butterworth IIR HPF');

~~~



## OUTPUT (LPF) :
<img width="1919" height="999" alt="Screenshot 2025-09-22 152028" src="https://github.com/user-attachments/assets/e9ff3bd9-d7b6-4a60-891e-3a7af3dd71fa" />

<img width="1919" height="1002" alt="Screenshot 2025-09-22 152042" src="https://github.com/user-attachments/assets/3e82138c-b026-4d58-bc95-7c6024c43358" />

<img width="1917" height="1078" alt="Screenshot 2025-09-22 152335" src="https://github.com/user-attachments/assets/95240509-a8ec-4298-bd1e-a997accd0602" />


## OUTPUT (HPF) : 
<img width="1917" height="1069" alt="Screenshot 2025-09-22 152608" src="https://github.com/user-attachments/assets/824524e7-3a2d-4095-9304-b41d38a61761" />

<img width="1918" height="1077" alt="Screenshot 2025-09-22 152618" src="https://github.com/user-attachments/assets/4fa0eab6-09b2-491c-aba4-e92586f6eeed" />

<img width="1918" height="1072" alt="Screenshot 2025-09-22 152628" src="https://github.com/user-attachments/assets/585cf5ae-13a5-401a-852a-4b2e9607f6dc" />




## RESULT:
To design an IIR Butterworth filter (LPF & HPF) using SCILAB was successfully ececuted.
