clear all;
clc

%1.Grey level transformation
OP = imread('X:\DIP\assignment2\oldpic.bmp');
OP=im2double(OP); 
OP = rgb2gray(OP);  %change to gray figure
subplot(2,2,1)
imshow(OP);
title("Origion");

%Segmental Linear Transformation 
for i = 1:256
    for j = 1:256
        if(OP(i,j)<=140)
            OP_SLT(i,j) = 0.8.*OP(i,j);        
        end
        if( OP(i,j)>140)
            OP_SLT(i,j) = 1.2.*OP(i,j) - 60;
        end
    end
end
subplot(2,2,2)
imshow(OP_SLT);
title("Segmental Linear Transformation");

%Gamma Transformation 
gamma = 2;
k = 0.8;
OP_GT = k * (OP .^ gamma);
subplot(2,2,3)
imshow(OP_GT);
title("Gamma=2 Transformation");
%Better version for gamma transformation
gamma = 3;
k = 1;
OP_GT = k * (OP .^ gamma);
subplot(2,2,4)
imshow(OP_GT);
title("Gamma=3 Transformation");

%2.Bitplane stratification
Lena = imread('X:\DIP\assignment2\Lena.bmp');
[a,b] = size(Lena);
subplot(3,3,1)
imshow(Lena);
for t=1:8
    for i=1:a
        for j=1:b
            if(Lena(i,j)>=2.^(t-1) && Lena(i,j)<2.^t)
                L(i,j)=255;
            else
                L(i,j)=0;
            end
        end
    end
subplot(3,3,t+1)
imshow(L);
end

%3.Column diagram 
CM = imread('X:\DIP\assignment2\cameraman.bmp'); 
for t = 1:1:256
    k(t)=0;
    for i = 1:1:256
        for j = 1:1:256
            if(CM(i,j)==t)
                k(t)=k(t)+1;
            end
        end
    end
end
bar(k,0.2);
%or imhist(CM);

%4.Histogram equalization 
CM = imread('X:\DIP\assignment2\cameraman.bmp'); 
CM_HE = histeq(CM);
imshow(CM_HE);
imwrite(CM_HE,'X:\DIP\assignment2\CM_HE.bmp');