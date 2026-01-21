# 🔐 Generador de Códigos Taquillas - GitHub Actions

Ejecuta 8 jobs en paralelo para generar los códigos de los 128 lockers.

## ⏱️ Tiempo estimado

| Códigos/locker | Tiempo por job | Tiempo TOTAL (paralelo) |
|----------------|----------------|-------------------------|
| 100            | ~20 min        | ~20 min                 |
| 500            | ~1.5 horas     | ~1.5 horas              |
| 1000           | ~3 horas       | ~3 horas                |

## 🚀 Setup (5 minutos)

### 1. Crear repositorio en GitHub

1. Ve a https://github.com/new
2. Nombre: `locker-codes-generator` (privado)
3. Crea el repo vacío

### 2. Subir archivos

Sube estos archivos al repo:
```
locker-codes-generator/
├── .github/
│   └── workflows/
│       └── scraper.yml
├── scraper.py
├── combine_results.py
└── README.md
```

**Opción fácil:** Arrastra los archivos directamente en GitHub web.

### 3. Configurar Secrets

Ve a tu repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

Crea estos 2 secrets:

| Nombre | Valor |
|--------|-------|
| `LOCKER_EMAIL` | `Nacho@thebassementclub.com` |
| `LOCKER_PASSWORD` | `FundaVerde` |

### 4. Ejecutar

1. Ve a la pestaña **Actions** en tu repo
2. Click en **"Generar Códigos Taquillas"** (izquierda)
3. Click en **"Run workflow"** (derecha)
4. Introduce el número de códigos (ej: `500`)
5. Click **"Run workflow"** verde

### 5. Descargar resultados

Cuando termine (~1-3 horas):
1. Ve a **Actions** → click en la ejecución completada
2. Baja hasta **Artifacts**
3. Descarga **"CODIGOS_COMPLETOS_128_LOCKERS"**

## 📊 Estructura del resultado

El Excel final tendrá este formato:

| Locker # | Serial | código 0 | código 1 | código 2 | ... | código 499 |
|----------|--------|----------|----------|----------|-----|------------|
| 1        | 000001 | 1234     | 5678     | 9012     | ... | 3456       |
| 2        | 000002 | 2345     | 6789     | 0123     | ... | 4567       |
| ...      | ...    | ...      | ...      | ...      | ... | ...        |
| 128      | 000128 | 8901     | 2345     | 6789     | ... | 0123       |

## 🔧 Personalización

### Cambiar número de códigos por defecto

En `scraper.yml`, línea 11:
```yaml
default: '500'  # Cambiar a lo que quieras
```

### Ejecutar solo algunos lockers

Puedes modificar la matriz en `scraper.yml` para procesar solo ciertos rangos.

## ❓ Troubleshooting

**"Login falló"**: Verifica que los secrets están bien configurados.

**Un job falló pero los demás siguieron**: Es normal, los resultados parciales se guardan.

**Timeout (6 horas)**: Reduce el número de códigos o divide en más batches.

## 💰 Costes

- **GitHub Actions**: 2000 min/mes gratis en repos privados
- **Esta ejecución**: ~500-1000 min (según códigos)
- **Total: GRATIS** (si no excedes el límite mensual)
