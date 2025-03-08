

### 1. econocimiento de la Empresa u Organización

**Objetivo**: Identificar la entidad propietaria del dominio y obtener información básica sobre la empresa u organización asociada.

#### Pasos en Maltego:

- **Transformación: `To WHOIS Record`**: Obtén el registro WHOIS del dominio para identificar al propietario.
- **Transformación: `To Email Address [From WHOIS]`**: Extrae direcciones de correo electrónico del registro WHOIS.

#### Herramientas Adicionales:

- **Whois Lookup**: Utiliza servicios como Whois.net para obtener información adicional del registro WHOIS.

### 2. Identificación de Actores Clave

**Objetivo**: Identificar actores clave dentro de la empresa, como personal ejecutivo, equipos de seguridad, y otros contactos relevantes.

#### Pasos en Maltego:

- **Transformación: `To Person [From Email Address]`**: Identifica personas asociadas a las direcciones de correo electrónico obtenidas.
- **Transformación: `To Social Network Profiles`**: Encuentra perfiles de redes sociales asociados a las direcciones de correo electrónico.

#### Herramientas Adicionales:

- **LinkedIn**: Busca perfiles de empleados y ejecutivos en LinkedIn.
- **Hunter.io**: Encuentra direcciones de correo electrónico asociadas a un dominio.

### 3. Recopilación de Información Pública

**Objetivo**: Obtener información pública disponible sobre la empresa, como ubicaciones de oficinas, números de contacto, y detalles de contacto.

#### Pasos en Maltego:

- **Transformación: `To DNS Name`**: Obtén nombres DNS asociados al dominio.
- **Transformación: `To MX Records`**: Obtén los registros MX del dominio para identificar servidores de correo.

#### Herramientas Adicionales:

- **Google Search**: Realiza búsquedas específicas para encontrar información pública sobre la empresa.
- **Company Websites**: Visita el sitio web oficial de la empresa para obtener detalles de contacto y ubicaciones.

### 4. Análisis de Redes Sociales

**Objetivo**: Explorar la presencia en redes sociales asociada con el dominio para comprender mejor la interacción y la percepción pública.

#### Pasos en Maltego:

- **Transformación: `To Social Network Profiles`**: Encuentra perfiles de redes sociales asociados a las direcciones de correo electrónico obtenidas.

#### Herramientas Adicionales:

- **Social Searcher**: Utiliza herramientas como Social Searcher para monitorear menciones en redes sociales.
- **Twitter Advanced Search**: Realiza búsquedas avanzadas en Twitter para encontrar menciones y perfiles relacionados con el dominio.

### 5. Reconocimiento Competitivo

**Objetivo**: Obtener información sobre la competencia y su presencia en línea mediante la identificación de dominios relacionados.

#### Pasos en Maltego:

- **Transformación: `To DNS Name [Subdomains]`**: Descubre subdominios asociados al dominio.
- **Transformación: `To IP Address [From DNS Name]`**: Obtén direcciones IP adicionales asociadas a los nombres DNS.

#### Herramientas Adicionales:

- **SimilarWeb**: Utiliza SimilarWeb para analizar la presencia en línea de la competencia.
- **BuiltWith**: Utiliza BuiltWith para obtener información sobre la tecnología utilizada por los sitios web de la competencia.

### 6. Inteligencia Competitiva

**Objetivo**: Recopilar información sobre la estrategia digital, productos, servicios y actividades en línea de la competencia.

#### Pasos en Maltego:

- **Transformación: `To DNS Name`**: Obtén nombres DNS asociados al dominio.
- **Transformación: `To IP Address [DNS]`**: Obtén la dirección IP del dominio.

#### Herramientas Adicionales:

- **Google Alerts**: Configura alertas de Google para monitorear menciones de la competencia.
- **Ahrefs**: Utiliza Ahrefs para analizar la estrategia de SEO y contenido de la competencia.

### 7. Cumplimiento Normativo

**Objetivo**: Evaluar si el dominio y la empresa cumplen con requisitos normativos específicos, como políticas de privacidad en línea.

#### Pasos en Maltego:

- **Transformación: `To WHOIS Record`**: Obtén el registro WHOIS del dominio para verificar la información de contacto y cumplimiento normativo.

#### Herramientas Adicionales:

- **Privacy Policies**: Revisa las políticas de privacidad en el sitio web de la empresa.
- **GDPR Compliance Tools**: Utiliza herramientas de cumplimiento de GDPR para evaluar la conformidad con las normativas de protección de datos.

### Creación de Entidades y Relaciones

- **Crear Entidades y Relaciones**: Asegúrate de crear todas las entidades y relaciones con sus respectivas anotaciones, propiedades y etiquetas en Maltego.
- **Exportar el Grafo**: Exporta el grafo en formato .mtgl para su entrega.

### Entrega del Trabajo

- **Memoria del Trabajo**: Redacta una memoria detallada del trabajo realizado, incluyendo los pasos seguidos, las herramientas utilizadas y los hallazgos obtenidos.
- **Fichero .mtgl**: Entrega el fichero .mtgl con el grafo generado en Maltego.

Espero que esta guía te sea útil para completar tu práctica. ¿Hay algo más en lo que te pueda ayudar? 😊