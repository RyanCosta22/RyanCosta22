!pip install Pillow cryptography

from PIL import Image
from cryptography.fernet import Fernet
import hashlib
import base64
import os

# Função para gerar chave para criptografia
def generate_key():
    key = Fernet.generate_key()
    with open("secret.key", "wb") as key_file:
        key_file.write(key)

# Função para carregar a chave
def load_key():
    return open("secret.key", "rb").read()

# Função para criptografar mensagem
def encrypt_message(message):
    key = load_key()
    f = Fernet(key)
    encrypted_message = f.encrypt(message.encode())
    return encrypted_message

# Função para descriptografar mensagem
def decrypt_message(encrypted_message):
    key = load_key()
    f = Fernet(key)
    decrypted_message = f.decrypt(encrypted_message).decode()
    return decrypted_message

# Função para converter mensagem em binário
def message_to_binary(message):
    return ''.join(format(ord(char), '08b') for char in message)

# Função para converter binário em mensagem
def binary_to_message(binary_data):
    chars = [binary_data[i:i + 8] for i in range(0, len(binary_data), 8)]
    return ''.join(chr(int(char, 2)) for char in chars)

# Função para embutir mensagem em imagem
def embed_text_in_image(image_path, message, output_image_path):
    image = Image.open(image_path)
    binary_message = message_to_binary(message) + '1111111111111110'  # Sequência de terminação
    data_index = 0

    pixels = image.load()
    for row in range(image.size[1]):
        for col in range(image.size[0]):
            if data_index < len(binary_message):
                r, g, b = pixels[col, row]
                r = (r & 254) | int(binary_message[data_index])
                data_index += 1

                if data_index < len(binary_message):
                    g = (g & 254) | int(binary_message[data_index])
                    data_index += 1

                if data_index < len(binary_message):
                    b = (b & 254) | int(binary_message[data_index])
                    data_index += 1

                pixels[col, row] = (r, g, b)

    image.save(output_image_path)

# Função para recuperar mensagem de uma imagem
def decode_text_from_image(image_path):
    image = Image.open(image_path)
    binary_message = ''
    pixels = image.load()
    for row in range(image.size[1]):
        for col in range(image.size[0]):
            r, g, b = pixels[col, row]
            binary_message += str(r & 1)
            binary_message += str(g & 1)
            binary_message += str(b & 1)

    termination_index = binary_message.find('1111111111111110')
    if termination_index != -1:
        binary_message = binary_message[:termination_index]
    return binary_to_message(binary_message)

# Função para gerar hash da imagem
def generate_image_hash(image_path):
    with open(image_path, "rb") as image_file:
        image_data = image_file.read()
    return hashlib.sha256(image_data).hexdigest()

# Função principal de menu
def main():
    generate_key()  # Gere a chave ao iniciar
    while True:
        print("\nMenu de Opções:")
        print("(1) Embutir texto em uma imagem")
        print("(2) Recuperar texto de uma imagem")
        print("(3) Gerar hash das imagens")
        print("(4) Encriptar mensagem")
        print("(5) Decriptar mensagem")
        print("(S ou s) Para sair")

        choice = input("Escolha uma opção: ")

        if choice in ['S', 's']:
            print("Saindo...")
            break

        if choice == '1':
            image_path = input("Caminho da imagem: ")
            message = input("Mensagem a embutir: ")
            output_image_path = input("Caminho da imagem de saída: ")
            embed_text_in_image(image_path, message, output_image_path)
            print("Mensagem embutida com sucesso!")

        elif choice == '2':
            image_path = input("Caminho da imagem: ")
            recovered_message = decode_text_from_image(image_path)
            print("Mensagem recuperada:", recovered_message)

        elif choice == '3':
            original_image_path = input("Caminho da imagem original: ")
            altered_image_path = input("Caminho da imagem alterada: ")
            original_hash = generate_image_hash(original_image_path)
            altered_hash = generate_image_hash(altered_image_path)
            print("Hash da imagem original:", original_hash)
            print("Hash da imagem alterada:", altered_hash)

        elif choice == '4':
            message = input("Mensagem a encriptar: ")
            encrypted_message = encrypt_message(message)
            print("Mensagem encriptada:", encrypted_message)

        elif choice == '5':
            encrypted_message = input("Mensagem encriptada: ")
            decrypted_message = decrypt_message(encrypted_message.encode())
            print("Mensagem decriptada:", decrypted_message)

        else:
            print("Opção inválida! Tente novamente.")

# Executa a função principal
main()
