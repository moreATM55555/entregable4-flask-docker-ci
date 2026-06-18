# PROYECTO ENTREGABLE 4 - CRISTIAN MORENO LOPEZ

## Descripción del proyecto

Este proyecto consiste en una aplicación web sencilla desarrollada con **Flask**, contenerizada mediante **Docker** y desplegada de forma automática a través de un *pipeline* de integración continua configurado con **GitHub Actions**.

La aplicación responde con un mensaje de saludo al acceder a la ruta raíz (`/`). El pipeline se encarga de descargar el código, ejecutar las pruebas unitarias con **pytest**, construir la imagen Docker y subirla a **Docker Hub** automáticamente cada vez que se realiza un *push* a la rama `main`.

## Estructura del repositorio

```
entregable4-flask-docker-ci/
│
├── app.py                          # Aplicación Flask
├── test_app.py                     # Pruebas unitarias con pytest
├── requirements.txt                # Dependencias del proyecto
├── Dockerfile                      # Definición de la imagen Docker
├── .github/
│   └── workflows/
│       └── pipeline.yml            # Pipeline de CI/CD con GitHub Actions
└── README.md                       # Este archivo
```

## Tecnologías utilizadas

- **Python 3.12**
- **Flask** — framework web
- **pytest** — pruebas unitarias
- **Docker** — contenerización
- **GitHub Actions** — integración continua y despliegue
- **Docker Hub** — registro de imágenes

## Cómo ejecutar la aplicación en local (sin Docker)

```bash
# Crear y activar un entorno virtual (opcional pero recomendado)
python -m venv venv
source venv/bin/activate      # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar la aplicación
python app.py
```

La aplicación quedará disponible en `http://localhost:5000`.

## Cómo ejecutar las pruebas unitarias

```bash
pytest -v
```

## Cómo construir y ejecutar la imagen Docker en local

```bash
# Construir la imagen
docker build -t flask-ci-app .

# Ejecutar el contenedor
docker run -p 5000:5000 flask-ci-app
```

La aplicación quedará disponible en `http://localhost:5000`.

## Cómo descargar y ejecutar la imagen ya publicada en Docker Hub

```bash
docker pull cristianmor99/flask-ci-app:latest
docker run -p 5000:5000 cristianmor99/flask-ci-app:latest
```

## Pipeline de integración continua

El pipeline definido en `.github/workflows/pipeline.yml` se ejecuta automáticamente en cada `push` o `pull request` a la rama `main`, y consta de dos etapas (*jobs*):

1. **test**: descarga el código, instala las dependencias y ejecuta las pruebas unitarias con pytest.
2. **build-and-push**: si las pruebas pasan correctamente, construye la imagen Docker a partir del `Dockerfile` y la sube a Docker Hub.

### Configuración necesaria en GitHub

Para que el pipeline pueda autenticarse en Docker Hub, es necesario configurar los siguientes *secrets* en el repositorio (`Settings → Secrets and variables → Actions → New repository secret`):

| Secret              | Valor                                              |
| ------------------- | --------------------------------------------------- |
| `DOCKERHUB_USERNAME` | Nombre de usuario de Docker Hub (`cristianmor99`) |
| `DOCKERHUB_TOKEN`   | Access Token generado en Docker Hub (no la contraseña) |

## Autor

Cristian Moreno López

## Enlace a repositorio

https://github.com/moreATM55555/entregable4-flask-docker-ci
