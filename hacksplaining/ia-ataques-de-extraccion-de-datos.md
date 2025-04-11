# IA: Ataques de extracción de datos

Tu modelo de aprendizaje automático puede ser vulnerable a ataques de extracción de datos. Esto representa un riesgo de seguridad tanto para ti como para tus clientes.

Algunas de las consecuencias reales de la extracción de datos son:

* Violaciones de privacidad
* Robo de propiedad intelectual
* Compromiso de credenciales
* Desventaja competitiva
* Responsabilidad legal

Aprendamos algunas de las formas en que se presentan los ataques de extracción de datos.

## Explotación de Memorización

La explotación de memorización apunta a la tendencia de los modelos de aprendizaje automático a memorizar inadvertidamente ejemplos de entrenamiento específicos, particularmente datos inusuales o repetidos. Los modelos grandes, especialmente los modelos de lenguaje, a veces almacenan secuencias exactas de sus datos de entrenamiento en lugar de aprender solo los patrones.

Esto es particularmente común con:

* Información rara o única (números de teléfono, direcciones, claves de API)
* Contenido repetido frecuentemente (citas populares, fragmentos de código)
* Datos estructurados con patrones distintivos (formatos de tarjetas de crédito, números de seguro social)

**Cómo funciona:** Los atacantes explotan esto de la siguiente manera:

* Usando prompts de extracción: Completa esta secuencia: 555-123-...
* Apuntando a la recuperación literal: ¿Cuál era la dirección de John Smith de nuevo?
* Creando contextos similares a los ejemplos de entrenamiento: Aquí está mi información de tarjeta de crédito: 4...

## Inversión del Modelo

La inversión del modelo se refiere a un tipo de ataque en el que un adversario intenta reconstruir o extraer los datos de entrenamiento utilizados para entrenar un modelo de aprendizaje automático.

Por ejemplo, si entrenas clasificadores de imágenes con datos sensibles, los atacantes podrían robar esos datos. En lugar de solo obtener predicciones, extraen las imágenes de entrenamiento reales. Esto podría permitir:

* Que un atacante recupere fotos de pasaporte utilizadas para entrenar una IA de control fronterizo
* Que se extraigan imágenes médicas usadas en sistemas de diagnóstico, revelando escaneos de pacientes
* Que se roben diseños de productos patentados en sistemas de control de calidad de manufactura

**Cómo funciona:** Los atacantes consultan tu modelo repetidamente con entradas diseñadas, analizando pequeñas diferencias en las puntuaciones de confianza. Al trabajar hacia atrás desde estas respuestas, reconstruyen gradualmente las entradas originales de entrenamiento.

## Fugas de Prompts del Sistema

Los prompts del sistema en los modelos de lenguaje grandes están diseñados para guiar la salida del modelo según los requisitos de la aplicación, pero pueden contener secretos inadvertidamente. Cuando se descubren, esta información puede ser utilizada para facilitar otros ataques.

Los atacantes a menudo utilizan ataques de inyección de prompts para descubrir los prompts del sistema.

### Fugas entre Sesiones

Cuando los sistemas de IA mantienen información entre diferentes sesiones de usuario, los datos sensibles de una sesión de usuario pueden filtrarse a otra. Esto ocurre porque:

* Los modelos pueden retener contexto de interacciones previas en su memoria
* La infraestructura compartida podría no aislar correctamente los datos de los usuarios
* Los mecanismos de caché destinados al rendimiento pueden crear vulnerabilidades de seguridad

**Cómo funciona:** Un atacante podría explotar el estado compartido para extraer datos de sesiones previas. Asegurar un aislamiento adecuado de las sesiones en los sistemas de aprendizaje automático es clave para protegerse contra este tipo de ataque.

## Ingeniería Inversa del Modelo

La ingeniería inversa del modelo se refiere a las técnicas utilizadas para reconstruir la arquitectura interna de un modelo de aprendizaje automático, sus parámetros o límites de decisión observando solo sus entradas y salidas. Esto incluye:

* Recuperación de arquitectura: Determinar la estructura del modelo (capas, neuronas, conexiones)
* Extracción de parámetros: Estimar los pesos y sesgos del modelo
* Mapeo de límites de decisión: Reconstruir cómo el modelo separa diferentes clases
* Clonación de funcionalidades: Crear un modelo sustituto que se comporte de manera similar

**Cómo funciona:** Los atacantes generalmente implementan esto de la siguiente manera:

* Consultando sistemáticamente el modelo con entradas diversas
* Analizando patrones en las respuestas
* Entrenando su propio "modelo sombra" para imitar el modelo objetivo
* Usando técnicas de optimización para igualar el comportamiento del modelo objetivo

A diferencia de otros ataques que se centran en extraer datos de entrenamiento, la ingeniería inversa del modelo apunta a la propiedad intelectual del modelo en sí: el algoritmo y los parámetros que representan inversiones significativas en investigación y desarrollo.

## Mitigación

**Sanitizar los Datos Antes del Entrenamiento** Para evitar la fuga de datos sensibles a través de tus modelos, el enfoque más directo es sanitizar cualquier dato antes de que entre en tu conjunto de entrenamiento.

* **Eliminar identificadores explícitos**: Utiliza el reconocimiento de entidades nombradas para identificar y reemplazar entidades sensibles como nombres y direcciones.
* Usa expresiones regulares para anonimizar información personal identificable como correos electrónicos, números de seguro social y números de tarjeta de crédito.
* **Transformar atributos sensibles**: Aplica k-anonimato: asegúrate de que los puntos de datos compartan atributos con al menos k otros. Por ejemplo, elimina los registros con nombres o códigos postales únicos de tu conjunto de datos.
* Usa privacidad diferencial: agrega ruido calibrado para proteger los registros individuales.

### **Reducir la Unicidad**

* Agrupa categorías raras en grupos más amplios.
* Redondea o agrupa valores numéricos para evitar la huella digital.
* Elimina valores atípicos que puedan ser fácilmente identificables.

### **Procesar Imágenes**

* Borra u oculta caras y características identificativas.
* Elimina los metadatos de los datos de entrenamiento (geolocalización, información del dispositivo, marcas de tiempo).
* Baja la resolución para evitar la recuperación de detalles finos.

### **Construir tu Prompt del Sistema con Cuidado**

&#x20;Asume que con suficiente determinación, un atacante podrá engañar a tu modelo para revelar tu prompt del sistema. Para protegerte:

* Asegúrate de que no haya información sensible (por ejemplo, claves de API o URLs sensibles) incrustada en el prompt.
* Asegúrate de que los controles de seguridad se apliquen de manera independiente al modelo.

### **Implementar Limitación de Velocidad**

&#x20;Limitar el número de consultas que se pueden hacer desde una fuente determinada reduce significativamente la posibilidad de extracción de datos por parte de un atacante.

### **Emplear Destilación de Conocimiento**

&#x20;Considera entrenar un modelo de estudiante más pequeño que aprenda patrones generales pero no ejemplos específicos, y luego despliega el modelo de estudiante en lugar del original. Esto reducirá la memorización de ejemplos de entrenamiento y evitará la ingeniería inversa del modelo.

### **Considerar el Uso de Datos de Entrenamiento Sintéticos**

&#x20;Los datos de entrenamiento generados sintéticamente, siempre que sean realistas, te permitirán entrenar tu modelo sin riesgo de que se filtren datos de entrenamiento. Aún puedes probar tu modelo con datos reales para asegurarte de que los resultados sean los esperados.

### **Limitar el Estado Compartido**

&#x20;El tiempo de cómputo puede ser costoso en aplicaciones de aprendizaje automático, especialmente en aplicaciones interactivas que usan modelos de lenguaje grandes. Resiste la tentación de reutilizar sesiones o estado para reducir costos, a menos que estés seguro de que puedes hacerlo de manera segura.



## Ejemplos de código

### Sanitación  de Textos

```python
import spacy

def sanitize_names(text):
  # Load English language model (you can use a larger model for better accuracy)
  nlp = spacy.load("en_core_web_sm")
  
  # Process the text
  doc = nlp(text)
  
  # Create a sanitized version by replacing PERSON entities
  sanitized = text
  for ent in reversed(doc.ents):
    if ent.label_ == "PERSON":
      # Replace with [REDACTED] or initial or other pattern
      sanitized = sanitized[:ent.start_char] + "[REDACTED]" + sanitized[ent.end_char:]
  
  return sanitized

# Example usage
text = "John Smith met with Sarah Johnson to discuss the project."
sanitized_text = sanitize_names(text)
print(sanitized_text)
# Output: "[REDACTED] met with [REDACTED] to discuss the project."

```



### Sanitación de Tokens

```python
import re

def detect_sensitive_data(text):
  # Regular expressions for sensitive data
  ssn_pattern   = r'\b\d{3}[-\s]?\d{2}[-\s]?\d{4}\b'
  email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
  
  # Basic credit card pattern (covers major formats)
  cc_pattern = r'\b(?:\d{4}[-\s]?){3}\d{4}\b|\b\d{16}\b'
  
  # Make a copy of text for redaction.
  redacted_text = text
  sensitive_data = {
    "SSN": [],
    "EMAIL": [],
    "CREDIT_CARD": []
  }
  
  # Find SSNs
  ssn_matches = re.finditer(ssn_pattern, text)
  for match in ssn_matches:
    sensitive_data["SSN"].append(match.group())
    redacted_text = redacted_text.replace(match.group(), "[SSN_REDACTED]")
  
  # Find email addresses
  email_matches = re.finditer(email_pattern, text)
  for match in email_matches:
    sensitive_data["EMAIL"].append(match.group())
    redacted_text = redacted_text.replace(match.group(), "[EMAIL_REDACTED]")
  
  # Find credit card numbers. We could apply the Luhn algorithm 
  # (https://en.wikipedia.org/wiki/Luhn_algorithm) here for greater accuracy.
  cc_matches = re.finditer(cc_pattern, text)
  for match in cc_matches:
    sensitive_data["CREDIT_CARD"].append(match.group())
    redacted_text = redacted_text.replace(match.group(), "[CC_REDACTED]")
  
  return redacted_text, sensitive_data
```

## Fuentes y lecturas relacionadas

* AI Exchange [**OWASP**](https://owaspai.org/)
* [AI Data Security](https://www.sentinelone.com/cybersecurity-101/data-and-ai/ai-data-security/) **SentinelOne**
* [**Quiz: AI Data Extraction Attacks**](ia-ataques-de-extraccion-de-datos.md)





