# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 05

### Modelo de la bomba 3.0

La bomba está representada con una máquina de estados que tiene tres estados principales:

**CONFIG:** permite ajustar el tiempo de la cuenta regresiva con los botones A y B, se pasa al estado ARMED cuando ocurre el evento S

**ARMED:** inicia la cuenta regresiva, cada segundo disminuye el contador. Si se ingresa la secuencia correcta de desactivación (A-B-A), regresa a CONFIG. Si el contador llega a cero, pasa al estado EXPLODED.

**EXPLODED:** la bomba muestra el ícono de calavera. Solo puede regresar a CONFIG cuando ocurre el evento T


| Estado inicial | Evento disparador | Acciones esperadas | Estado final |
| --- | --- | --- | --- |
| CONFIG | A | Incrementar count en 1 (máx. 60) y mostrar en pantalla | CONFIG |
| CONFIG | B | Decrementar count en 1 (mín. 10) y mostrar en pantalla | CONFIG |
| CONFIG | S (shake) | Guardar tiempo inicial e iniciar cuenta regresiva | ARMED |
| ARMED | Tick de 1s | Decrementar count en 1 y mostrar en pantalla | ARMED |
| ARMED | Tick con count=0 | Mostrar calavera | EXPLODED |
| ARMED | Secuencia A-B-A correcta | Reiniciar count en 20 y mostrarlo | CONFIG |
| ARMED | Secuencia A-B-A incorrecta | Reiniciar índice de secuencia y continuar cuenta | ARMED |
| EXPLODED | T (touch) | Reiniciar count en 20 y mostrarlo | CONFIG |

<img width="800" height="800" alt="Screenshot 2025-08-19 073543" src="https://github.com/user-attachments/assets/69fe7149-592e-4050-b221-a35c52091a2b" />


