# n8n con PostgreSQL Vectorial

Configuración para desplegar n8n con una base de datos PostgreSQL habilitada para almacenamiento vectorial. Esta configuración permite usar n8n con capacidades de memoria para LLMs y búsqueda semántica.

## 🚀 Despliegue Rápido

1. Clona y configura:
```bash
git clone [URL_DEL_REPOSITORIO]
cd n8n-synapse
cp .env.example .env
nano .env  # Configura tus credenciales
```

2. Inicia los servicios:
```bash
docker compose up -d
```

3. Accede a n8n:
```
http://localhost:5678
```

## 🔧 Componentes

- **n8n**: Plataforma de automatización
- **PostgreSQL**: Base de datos con pgvector
- **Tabla embeddings**: Estructura para vectores

## 🗄️ Estructura de Datos

```sql
CREATE TABLE embeddings (
    id SERIAL PRIMARY KEY,
    content TEXT NOT NULL,
    embedding vector(1536),
    metadata JSONB,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);
```

## 📝 Uso Básico

### Insertar Datos
```sql
INSERT INTO embeddings (content, embedding, metadata)
VALUES ('texto', '[vector]', '{"fuente": "doc"}');
```

### Buscar Similares
```sql
SELECT content, metadata
FROM embeddings
ORDER BY embedding <=> '[vector]'
LIMIT 5;
```

## 🔒 Variables de Entorno

```env
POSTGRES_PASSWORD=password
N8N_USER=admin
N8N_PASS=password
SERVER_IP=localhost
```

## 📚 Recursos

- [n8n Docs](https://docs.n8n.io/)
- [pgvector Docs](https://github.com/pgvector/pgvector) 