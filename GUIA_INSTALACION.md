# Guía de Instalación - Chatbot IA Pymes

## 🚀 Pasos Iniciales

### 1. Clonar el Repositorio
```bash
git clone https://github.com/ivansitoo69/Chat-bot-IA-pymes.git
cd Chat-bot-IA-pymes
```

### 2. Obtener API Key de Google Gemini

1. Ve a: https://makersuite.google.com/app/apikey
2. Click en "Create API Key" o "Get API key"
3. Copia tu clave
4. Guarda la clave en un lugar seguro

### 3. Configurar Variables de Entorno

#### Backend
```bash
cd backend
cp .env.example .env
```

Edita `backend/.env` y añade:
```
GEMINI_API_KEY=tu_api_key_aqui
DATABASE_URL=postgresql://chatbot_user:chatbot_password@localhost:5432/chatbot_db
JWT_SECRET=tu_secret_aleatorio_aqui
API_PORT=8000
DEBUG=True
```

#### Frontend
```bash
cd frontend
cp .env.example .env.local
```

Edita `frontend/.env.local`:
```
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## 🔧 Opción A: Instalación con Docker (Recomendado)

```bash
# En la raíz del proyecto
docker-compose up -d
```

Verifica:
- Backend: http://localhost:8000/docs
- Base de datos está corriendo en puerto 5432

---

## 💻 Opción B: Instalación Manual

### Backend (Python + FastAPI)

```bash
cd backend

# Crear ambiente virtual
python -m venv venv

# Activar ambiente virtual
# En Windows:
venv\Scripts\activate
# En macOS/Linux:
source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar servidor
python -m uvicorn app.main:app --reload
```

El backend estará en: **http://localhost:8000**

Documentación interactiva: **http://localhost:8000/docs**

### Frontend (React + Next.js)

```bash
cd frontend

# Instalar dependencias
npm install

# Ejecutar servidor de desarrollo
npm run dev
```

El frontend estará en: **http://localhost:3000**

### Base de Datos (Opcional - Para características avanzadas)

Necesitarás PostgreSQL instalado localmente o usa Docker:

```bash
docker run --name chatbot-postgres \
  -e POSTGRES_USER=chatbot_user \
  -e POSTGRES_PASSWORD=chatbot_password \
  -e POSTGRES_DB=chatbot_db \
  -p 5432:5432 \
  postgres:15-alpine
```

---

## ✅ Verificar que Todo Funciona

### 1. Verificar Backend
```bash
curl http://localhost:8000/api/health
```

Deberías ver:
```json
{
  "status": "ok",
  "message": "API funcionando correctamente"
}
```

### 2. Probar Gemini
```bash
curl http://localhost:8000/api/chat/test
```

Deberías ver una respuesta de Gemini.

### 3. Verificar Frontend
Abre: http://localhost:3000

---

## 🧪 Primeros Pasos

1. Abre http://localhost:3000 en tu navegador
2. Escribe un mensaje en el chat
3. ¡Debería recibir respuesta de la IA!

---

## 📝 Comandos Útiles

### Backend
```bash
# Ver logs en tiempo real
docker-compose logs -f backend

# Acceder a la base de datos
docker-compose exec postgres psql -U chatbot_user -d chatbot_db
```

### Frontend
```bash
# Build para producción
npm run build
npm run start
```

---

## 🆘 Troubleshooting

### Error: "GEMINI_API_KEY not found"
- Verifica que has creado el archivo `.env` en la carpeta backend
- Asegúrate de que has pegado tu API key correctamente
- No debe haber espacios extra

### Error: "Connection refused" en Puerto 8000
- Verifica que no hay otra aplicación usando el puerto 8000
- Mata el proceso: `lsof -i :8000` (macOS/Linux)

### Error: "Database connection failed"
- Verifica que PostgreSQL está corriendo
- Si usas Docker: `docker-compose up postgres -d`
- Verifica la DATABASE_URL en `.env`

---

## 🎯 Próximos Pasos

1. ✅ Instalar y configurar
2. ⬜ Crear interfaz frontend
3. ⬜ Agregar historial de conversaciones
4. ⬜ Integrar base de datos completa
5. ⬜ Agregar bot de Telegram
6. ⬜ Deploy en producción

¡Vamos a programar! 🚀
