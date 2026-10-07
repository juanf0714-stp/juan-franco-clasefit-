# Bitácora de uso de IA

## Herramientas que usé
1. Inicialmente usé ChatGPT para que me guiara en las instalaciones desde la terminal de mi Mac. En pocos minutos tenía a punto lo siguiente. También creé una carpeta para usarla como directorio activo en esta prueba.

    Homebrew  7.0.8       ✅<br>
    Node.js   26.10.0     ✅<br>
    npm       11.19.1     ✅<br>
    OpenSpec  1.14.1      ✅

3. Luego decidí usar Codex CLI porque se puede integrar con OpenSpec y me permite trabajar directamente sobre los archivos del proyecto desde la terminal (y por disponibilidad ya que está incluido en mi plan de ChatGPT).

4. Con Node.js, OpenSpec y Codex configurados, inicialicé el proyecto y dejé habilitadas las skills de OpenSpec, estableciendo el entorno necesario para comenzar el ejercicio y trabajar de forma iterativa con la IA bajo mi revisión y criterio.

5. Aunque era posible proporcionar a Codex los documentos completos de la prueba y solicitarle que generara los entregables, decidí trabajar de forma incremental. Proporcioné el contexto necesario en cada etapa y utilicé la IA como apoyo para explorar, estructurar y validar mis decisiones, manteniendo bajo mi responsabilidad el análisis del problema, el alcance, las reglas de negocio y los criterios de aceptación. Busqué reproducir un flujo de trabajo más cercano a una situación real de PO/BA.

## Prompts clave (3 a 5)
| # | Etapa (diseño / proposal / specs) | Prompt | Qué obtuve |
|---|---|---|---|
| 1 | Exploración/Diseño | $openspec-explore Te voy a pasar la transcripción de una conversación con Marcela, la dueña de un gimnasio ubicado en un barrio de Medellin. Quiero analizarla contigo como primer paso de diseño de producto, somos senior Product Owners expertos en proyectos de tecnología y en IA. <br><br> Ayúdame a entender bien el problema antes de pensar en la solución. A partir de la conversación, identifica: <br> - cuál es el problema principal y cuáles son los problemas secundarios;<br> - quiénes son los usuarios o actores involucrados y qué necesita cada uno;<br> - qué necesidades están explícitamente mencionadas;<br> - qué cosas quedan ambiguas o requieren una decisión de negocio;<br> - qué preguntas debería resolver un PO/BA antes de definir el MVP;<br> - qué casos límite o situaciones problemáticas deberíamos tener presentes. <br><br> No propongas todavía una solución ni conviertas el análisis en requisitos o user stories.<br> Distingue entre lo que está explícitamente dicho en la conversación y lo que estés infiriendo. Si algo no está claro, prefiero que lo señales para que iteremos en lugar de asumir de forma inmediata. | Una respuesta muy completa y detallada útil para ampliar la perspectiva del problema, clarificar actores, pero principalmente para ayudarme a evidenciar lo que debía o no hacer parte de un producto mínimo viable. <br><br> También fue clave ver qué elementos estaba dados explícitamente en el transcript y sobre cuáles debía realizar inferencias o direccionar con mis propias ideas.

| 1 | Exploración | |
| 1 | Exploración | |
| 1 | Exploración | |
| 1 | Exploración | |

## Lo que corregí o descarté
| # | Qué me entregó la IA | Qué hice yo | Por qué |
|---|---|---|---|
| 1 | Un resultado muy completo de exploración pero con mucha información poco relevante y demasiado amplia para la definición de un MVP | Seleccionar lo realmente relevante para atender el problema principal, por ejemplo de momento no atender la necesidad de pago desde el celular o las funciones de consulta para los instructores del gimnasio. También omitir supuestos que en términos reales no son tan críticos, como preocuparnos de si todos los clientes tiene acceso a internet y un celular para poder reservar sus clases | Porque esto no es clave para la definición de un mínimo viable, son aspectos que pueden ir a un backlog a futuro para entregas de valor incrementales o lo que conocemos como funcionalidades nice to have en las que inicialmente no nos generarían tanto valor como atender el problema principal. |
 

## Resultado de `openspec validate`
```
(pega aquí la salida)
```
