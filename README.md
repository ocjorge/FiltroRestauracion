# ImageRestorer

![Python](https://img.shields.io/badge/Python-3.7%2B-blue)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Active-success)
![Version](https://img.shields.io/badge/Version-1.0-orange)

Una herramienta de restauración de imágenes implementada en Python que aplica el filtro de Wiener para recuperar imágenes degradadas por ruido y desenfoque.

## 📋 Características

- Interfaz gráfica para selección de archivos de imagen
- Visualización comparativa entre la imagen original, degradada y restaurada
- Implementación del filtro de Wiener para restauración de imágenes
- Soporte para varios formatos de imagen (JPG, PNG, BMP, TIFF, GIF)
- Simulación de ruido gaussiano para fines de demostración

## 🚀 Instalación

1. Clona este repositorio:
   ```bash
   git clone https://github.com/usuario/ImageRestorer.git
   cd ImageRestorer
   ```

2. Instala las dependencias:
   ```bash
   pip install numpy opencv-python matplotlib scipy
   ```

## 💻 Uso

Ejecuta el programa:
```bash
python image_restorer.py
```

El programa:
1. Abrirá un cuadro de diálogo para seleccionar una imagen
2. Generará una versión degradada de la imagen (con ruido y desenfoque)
3. Aplicará el filtro de Wiener para restaurar la imagen
4. Mostrará las tres versiones (original, degradada y restaurada) en una única ventana

## 🧮 Fundamentos técnicos

El filtro de Wiener es un método de restauración de imágenes que opera en el dominio de la frecuencia, utilizando la Transformada Rápida de Fourier (FFT). Su objetivo es minimizar el error cuadrático medio entre la imagen original y la restaurada.

La fórmula del filtro de Wiener es:

```
W(u,v) = H*(u,v) / (|H(u,v)|² + K)
```

Donde:
- H*(u,v) es el conjugado complejo de la transformada de Fourier del kernel de degradación
- |H(u,v)|² es el cuadrado de la magnitud de la transformada
- K es un parámetro que controla el compromiso entre la eliminación del ruido y la nitidez

## 📷 Capturas de pantalla

![Ejemplo de restauración](https://via.placeholder.com/800x300?text=Ejemplo+de+restauración+de+imagen)

## 📊 Estructura del código

```
image_restorer.py      # Script principal
└── Funciones:
    ├── add_noise()    # Agrega ruido a la imagen (simulación)
    ├── wiener_filter()# Implementa el filtro de restauración
    └── main()         # Función principal del programa
```

## 🔧 Personalización

Puedes ajustar los siguientes parámetros para personalizar el rendimiento:

- `kernel_size`: Tamaño del kernel de desenfoque (default: 5)
- `K`: Parámetro de regularización del filtro Wiener (default: 0.01)
- `noise_type`: Tipo de ruido a aplicar ("gaussian" o "s&p" para sal y pimienta)

## 🤝 Contribuciones

Las contribuciones son bienvenidas! Puedes ayudar con:

1. Implementación de filtros de restauración adicionales
2. Mejoras en la interfaz de usuario
3. Optimización del rendimiento para imágenes grandes
4. Documentación y ejemplos adicionales

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

## 📚 Referencias

- [Restauración de imágenes digitales](https://en.wikipedia.org/wiki/Wiener_filter)
- [Filtro de Wiener](https://en.wikipedia.org/wiki/Wiener_filter)
- [Procesamiento digital de imágenes - Gonzalez & Woods](https://www.amazon.com/Digital-Image-Processing-Rafael-Gonzalez/dp/0133356728)
