import numpy as np
import matplotlib.pyplot as plt

img=plt.imread(r"c:\Users\user\Downloads\S__38060039_0.jpg")
plt.imshow(img)

img.shape # 674 rows, 1200columns, 3 channels (R,G,B) ...1D

img_gray=0.3*img[:,:,0]+0.6*img[:,:,1]+0.11*img[:,:,2]
plt.imshow(img_gray,cmap='gray')

FT=np.fft.fft2(img_gray)
FT_shift=np.fft.fftshift(FT)
plt.imshow(20*np.log(np.abs(FT_shift)),cmap='gray')

#LPF
[row,col]=img_gray.shape
c_row=row//2
c_col=col//2
FT_LPF=FT_shift[c_row-20:c_row+20,c_col-20:c_col+20]
FT_LPF_shift=np.fft.fftshift(FT_LPF)
FT_LPF_shift_if=np.fft.ifft2(FT_LPF_shift)
plt.imshow(np.real(FT_LPF_shift_if),cmap='gray')

FT_LPF.shape

np.fft.ifftshift(FT_LPF).shape

c_col

#HPF
[row,col]=img_gray.shape
c_row=row//2
c_col=col//2
FT_shift[c_row-40:c_row+40,c_col-40:c_col+40]=0
FT_HPF_shift=np.fft.ifftshift(FT_shift)
FT_LHF_shift_if=np.fft.ifft2(FT_HPF_shift)
plt.imshow(np.real(FT_LHF_shift_if),cmap='gray')
