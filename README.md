# ⚖️ Mejía & Asociados — Sitio web

Sitio corporativo estático del estudio jurídico **Mejía & Asociados**. Incluye:

- **Hero** con video de presentación y llamados a la acción
- **Servicios / áreas de práctica** (derecho comercial, arbitraje, protección patrimonial, entre otros)
- **Equipo** de abogados con foto y perfil
- **Conferencias** con videos
- **Clientes** asesorados
- **Contacto** con formulario y datos del estudio

## Cómo abrirlo

Es un sitio 100% **HTML + CSS** (sin build ni dependencias). Basta con abrir `index.html` en el navegador, o servirlo con cualquier servidor estático:

```bash
# opción 1: abrir directamente
open index.html

# opción 2: servidor local
python3 -m http.server 8000
```

## Estructura

```
index.html   # página única
style.css    # estilos (responsive)
img/         # logotipos, fotos del equipo y logos de clientes
```

Los videos del hero y de la sección de conferencias se cargan desde enlaces externos (Dropbox), por lo que se requiere conexión a internet para verlos.
