

import cv2
from google.colab.patches import cv2_imshow  # Substituto para cv2.imshow no Colab
import numpy as np # Importa a biblioteca NumPy

# Carregue a imagem colorida
imagem = cv2.imread('TesteMama.jpg')

# Separe os canais de cores
azul, verde, vermelho = cv2.split(imagem)

# Exiba a imagem original e cada canal separadamente
cv2_imshow(imagem)  # Imagem Original

# Exibir canais separados
cv2_imshow(cv2.merge([azul, np.zeros_like(azul), np.zeros_like(azul)]))  # Canal Azul
cv2_imshow(cv2.merge([np.zeros_like(verde), verde, np.zeros_like(verde)]))  # Canal Verde
cv2_imshow(cv2.merge([np.zeros_like(vermelho), np.zeros_like(vermelho), vermelho]))  # Canal Vermelho
     





import cv2
from skimage import io
from skimage.color import rgb2gray
from skimage.filters import threshold_otsu
from google.colab.patches import cv2_imshow

# Carregue a imagem
imagem = io.imread('TesteMama.jpg')

# Converta a imagem para escala de cinza
imagem_cinza = rgb2gray(imagem)

# Segmentação usando limiarização de Otsu
limiar = threshold_otsu(imagem_cinza)
imagem_segmentada = imagem_cinza > limiar

# Converta a imagem segmentada para o formato BGR (para visualização com OpenCV)
imagem_segmentada_bgr = (imagem_segmentada * 255).astype('uint8')

# Exiba a imagem original e a imagem segmentada
cv2_imshow(imagem)  # Imagem Original
cv2_imshow(imagem_segmentada_bgr)  # Imagem Segmentada

     



import cv2
import numpy as np
from skimage import io
from skimage.color import rgb2gray
from skimage.filters import threshold_otsu
from google.colab.patches import cv2_imshow

# Carregue a imagem
imagem = io.imread('TesteMama.jpg')

# Converta a imagem para escala de cinza
imagem_cinza = rgb2gray(imagem)

# Segmentação usando limiarização de Otsu
limiar = threshold_otsu(imagem_cinza)
imagem_segmentada = imagem_cinza > limiar

# Converta a imagem segmentada para o formato BGR (para visualização com OpenCV)
imagem_segmentada_bgr = (imagem_segmentada * 255).astype('uint8')

# Exiba a imagem segmentada
cv2_imshow(imagem_segmentada_bgr)

# Extração de características (exemplo: área do objeto)
area = cv2.countNonZero(imagem_segmentada_bgr)
print(f'Área detectada: {area} pixels')

# Inferir a presença de câncer com base na área detectada (exemplo simplificado)
if area > 5000:  # Este valor é arbitrário e deve ser ajustado conforme o caso
    print('Presença de câncer detectada.')
else:
    print('Ausência de câncer detectada.')

     

Área detectada: 357115 pixels
Presença de câncer detectada.

!git clone https://github.com/Raik22/Processamento-Digital-Faculdade.git
     
fatal: destination path 'Processamento-Digital-Faculdade' already exists and is not an empty directory.p
