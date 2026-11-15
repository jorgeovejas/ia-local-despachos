\# Día 1 · Ollama en Windows y primer modelo



\## Equipo

\- CPU: AMD Ryzen 5 5500U (6 núcleos / 12 hilos), sin GPU dedicada

\- RAM: 16 GB

\- Sistema: Windows, Ollama nativo



\## Instalación

\- Versión de Ollama: 0.40.16

\- Nube desactivada (OLLAMA\_NO\_CLOUD=1): sí 

\- Línea del registro: Ollama cloud disabled: true



\## Medición: qwen3.5:4b (sin razonamiento)

| Métrica | Valor |

| --- | --- |

| Memoria en RAM (ollama ps) | 3,1 GB |

| Procesador | 100 % CPU |

| Contexto | 4096 tokens |

| Lectura del prompt | 32,76 tokens/s |

| Escritura de la respuesta | 9,07 tokens/s |

| Tiempo total | 20,3 s |

| Uso de CPU (Administrador de tareas) | 48-50 % |

| Funciona en modo avión | sí |



\## Observaciones

\- Con razonamiento activado tarda mucho más: genera cientos de tokens ocultos.

\- Leer documentos sería el cuello de botella: 3.000 tokens ≈ 90 s en este equipo.

\- El modelo añade matices que no están en el texto («renovación», «obligatoriamente»).



\## Reto: memoria de un modelo de 8B a 4 bits



1\. Un parámetro a 4 bits ocupa 0,5 bytes.

2\. 8.000 millones × 0,5 = 4 GB, solo en parámetros. 

3\. Comprobación con mi modelo: 4.000 millones × 0,5 = 2 GB teóricos,

&#x20;  y ollama ps marca 3,1 GB. La diferencia se debe al contexto y a que no todo
   se comprime a 4 bits.

4\. Con mis programas habituales abiertos me quedan unos 4 GB libres; cerrándolos,

&#x20;  unos 9-10 GB. Un 8B (unos 4 GB más el contexto) cabe, pero justo.

&#x20;  Mi 4B va a 9 tokens/s; uno de 8B iría a unos 4-5 tokens/s, porque para cada

&#x20;  palabra hay que leer el doble de datos de la RAM.

