import numpy as np
import cv2
import matplotlib.pyplot as plt
from scipy import signal
import tkinter as tk
from tkinter import filedialog


def add_noise(image, noise_type="gaussian"):
    """Función para agregar ruido a la imagen (para demostración)"""
    if noise_type == "gaussian":
        row, col, ch = image.shape
        mean = 0
        sigma = 25
        gauss = np.random.normal(mean, sigma, (row, col, ch))
        noisy = image + gauss
        return np.clip(noisy, 0, 255).astype(np.uint8)
    elif noise_type == "s&p":
        row, col, ch = image.shape
        s_vs_p = 0.5
        amount = 0.05
        noisy = np.copy(image)

        # Sal (pixeles blancos)
        num_salt = np.ceil(amount * image.size * s_vs_p)
        coords = [np.random.randint(0, i - 1, int(num_salt)) for i in image.shape]
        noisy[coords[0], coords[1], :] = 255

        # Pimienta (pixeles negros)
        num_pepper = np.ceil(amount * image.size * (1. - s_vs_p))
        coords = [np.random.randint(0, i - 1, int(num_pepper)) for i in image.shape]
        noisy[coords[0], coords[1], :] = 0

        return noisy
    else:
        return image


def wiener_filter(img, kernel, K):
    """Implementación del filtro de Wiener para restauración"""
    kernel /= np.sum(kernel)
    dummy = np.copy(img)
    dummy = dummy.astype(float)

    # Aplicar transformada de Fourier a la imagen y al kernel
    img_fft = np.fft.fft2(dummy)
    kernel_fft = np.fft.fft2(kernel, s=img.shape)

    # Calcular el filtro de Wiener
    kernel_fft_abs = np.abs(kernel_fft) ** 2
    wiener = np.conj(kernel_fft) / (kernel_fft_abs + K)

    # Aplicar el filtro y obtener la imagen restaurada
    img_restored = np.fft.ifft2(img_fft * wiener)
    img_restored = np.abs(img_restored)

    return np.clip(img_restored, 0, 255).astype(np.uint8)


def main():
    # Crear una instancia de Tkinter (oculta)
    root = tk.Tk()
    root.withdraw()

    # Abrir el diálogo para seleccionar la imagen
    ruta_imagen = filedialog.askopenfilename(
        title="Selecciona una imagen",
        filetypes=[("Archivos de Imagen", "*.jpg *.jpeg *.png *.bmp *.tiff *.gif"),
                   ("Todos los archivos", "*.*")]
    )

    # Verificar si se seleccionó una imagen
    if not ruta_imagen:
        print("No se seleccionó ninguna imagen.")
        return

    # Leer la imagen seleccionada
    image = cv2.imread(ruta_imagen)
    if image is None:
        print(f"Error: No se pudo leer la imagen en {ruta_imagen}.")
        return

    # Convertir de BGR a RGB para visualización correcta
    image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

    # Crear una versión degradada (simular imagen con ruido o desenfoque)
    kernel_size = 5
    kernel = np.ones((kernel_size, kernel_size), np.float32) / (kernel_size * kernel_size)
    blurred = cv2.filter2D(image, -1, kernel)
    noisy_image = add_noise(blurred, "gaussian")

    # Aplicar el filtro de restauración (Wiener) por canal
    restored_image = np.zeros_like(noisy_image)
    for i in range(3):  # Para cada canal de color (R, G, B)
        restored_image[:, :, i] = wiener_filter(noisy_image[:, :, i], kernel, K=0.01)

    # Mostrar las imágenes
    plt.figure(figsize=(12, 6))

    plt.subplot(131)
    plt.title('Imagen Original')
    plt.imshow(image)
    plt.axis('off')

    plt.subplot(132)
    plt.title('Imagen Degradada')
    plt.imshow(noisy_image)
    plt.axis('off')

    plt.subplot(133)
    plt.title('Imagen Restaurada')
    plt.imshow(restored_image)
    plt.axis('off')

    plt.tight_layout()
    plt.show()


if __name__ == "__main__":
    main()
