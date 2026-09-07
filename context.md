# Contexto técnico

## Stack tecnológico

### Backend

- Python 3.13 sobre `python:3.13-slim`, definido en [backend/Dockerfile](backend/Dockerfile).
- FastAPI para la API HTTP.
- Uvicorn como servidor ASGI.
- Pydantic para modelos y validación de datos.
- `debugpy` para depuración remota en el puerto 5678.
- Pytest, pytest-cov y httpx para pruebas, declarados en [backend/requirements.txt](backend/requirements.txt).

### Frontend

- React 19.2 con `react-dom`.
- TypeScript 6.
- Vite 8 como servidor de desarrollo y bundler.
- Tailwind CSS 4 mediante `@tailwindcss/vite`.
- Recharts 3.8 para gráficos.
- Lucide React para iconos.
- Vitest 4 para pruebas.
- ESLint 9 con soporte para TypeScript, React Hooks y React Refresh.
- Node 24 sobre `node:24-alpine`, definido en [frontend/Dockerfile](frontend/Dockerfile).

### Orquestación

- Docker Compose con los servicios `frontend` y `backend`, definido en [docker-compose.yml](docker-compose.yml).
- Frontend expuesto en el puerto 5173.
- Backend expuesto en el puerto 8000.
- Debugger del backend expuesto en el puerto 5678.

## Scripts y comandos de arranque

### Arranque recomendado con Docker

Desde la raíz del proyecto:

```bash
docker compose up --build
```

URLs disponibles:

- Frontend: `http://localhost:5173`
- Backend: `http://localhost:8000`
- Documentación de la API: `http://localhost:8000/docs`

El comando está documentado en [README.es.md](README.es.md) y usa la configuración de [docker-compose.yml](docker-compose.yml).

### Backend

El comando de arranque definido en [backend/Dockerfile](backend/Dockerfile) es:

```bash
python -m debugpy --listen 0.0.0.0:5678 -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Para ejecutar las pruebas del backend:

```bash
pytest
```

### Frontend

Scripts definidos en [frontend/package.json](frontend/package.json):

```bash
npm run dev
npm run build
npm run lint
npm run preview
npm run test
npm run test:watch
npm run test:coverage
```

Significado de los scripts:

- `npm run dev`: inicia Vite en modo desarrollo.
- `npm run build`: ejecuta TypeScript y genera el build de producción con Vite.
- `npm run lint`: ejecuta ESLint.
- `npm run preview`: sirve localmente el build generado.
- `npm run test`: ejecuta Vitest una vez.
- `npm run test:watch`: ejecuta Vitest en modo observación.
- `npm run test:coverage`: ejecuta Vitest con cobertura.

El comando usado por el contenedor frontend es:

```bash
npm run dev -- --host 0.0.0.0 --port 5173
```
