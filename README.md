
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
     
