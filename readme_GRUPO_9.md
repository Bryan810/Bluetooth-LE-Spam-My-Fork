## 1. Relevancia con problemas reales de seguridad
El repositorio reproduce, en Android y sin hardware extra, el fenómeno de *popup-flooding* vía anuncios BLE que afectó a iOS 16/17 (ejemplo: modales de Apple TV/AirPods). Apple mitigó este vector en iOS 17.2 e iOS 18, por lo que es un caso real y documentado de ataque DoS a nivel de interfaz de usuario.  
*Citas:* [Apple actualizaciones](https://github.com/simondankelmann/Bluetooth-LE-Spam), artículos sobre vulnerabilidades BLE en iOS.

## 2. Cobertura multi-ecosistema
El proyecto no se limita a Apple. Genera tramas que disparan **Microsoft Swift Pair** (Windows) y **Samsung Easy Setup**. Esto amplía el alcance de pruebas y permite evaluar impactos en distintos ecosistemas a partir del mismo código base.  
*Cita:* [Microsoft Docs sobre Swift Pair](https://learn.microsoft.com/en-us/windows-hardware/drivers/bluetooth/).

## 3. Reproducibilidad y trazabilidad
- Código en **Kotlin**, licencia **GPL-3.0**.  
- Builds públicas: APK y distribución en **F-Droid**.  
- Requisitos mínimos: **Android 8+**.  
Esto asegura facilidad de auditoría, pruebas controladas y replicación en entornos de investigación.  

## 4. Alineado con la especificación BLE
El spam se fundamenta en **anuncios BLE (ADV_*)**, que son *broadcasts* sobre canales primarios 37/38/39.  
- En *legacy advertising*, el payload es de **31 bytes**.  
- En *extended advertising* (Bluetooth 5), puede ampliarse.  
Este diseño se ajusta al enfoque del repositorio (no-conectable, alta cadencia).  
*Cita:* Core Specification of Bluetooth SIG.

## 5. Control experimental y métricas
El proyecto sugiere intervalos de **20–100 ms** para el *advertising*, lo que permite:
- Medir ratio de pop-ups/min.  
- Evaluar freeze-time y latencia en la UI.  
- Comparar cargas entre móviles y hardware especializado (ej. Flipper Zero).  

## 6. Módulo defensivo (“Spam Detector”)
Incluye capacidad de detectar dispositivos emisores cercanos (incluido Flipper Zero) y notificar su presencia. Esto permite evaluar escenarios de **blue teaming** además del ataque, y abre camino a estudiar detección basada en patrones.  

## 7. Comparación con alternativas
- **AppleJuice**: centrado solo en ecosistema Apple.  
- **Flipper Zero**: requiere hardware externo.  
- **Bluetooth-LE-Spam**: mayor portabilidad (solo Android) + cobertura multi-ecosistema.  

## 8. Limitaciones conocidas
Android impone permisos y cuotas (`BLUETOOTH_ADVERTISE`, límites de instancias), lo que controla la intensidad del spam y hace el entorno más seguro para experimentación. Discutir estas restricciones forma parte del valor académico y ético del trabajo.  

---

## Conclusión
El repositorio **Bluetooth-LE-Spam** es idóneo para un trabajo de ciberseguridad porque:  
- Aborda un caso de vulnerabilidad real y documentada.  
- Facilita pruebas prácticas y reproducibles.  
- Integra escenarios ofensivos (spam) y defensivos (detección).  
- Permite análisis comparativos multi-ecosistema.
- Permite desctivcar parlantes bluetooth de vecinos molestos 

## Referencia
- Apple. (2023, diciembre 11). About the security content of iOS 17.2 and iPadOS 17.2. Apple Support. https://support.apple.com/en-us/HT214040
- Apple. (2024, septiembre 16). About the security content of iOS 18. Apple Support. https://support.apple.com/en-us/HT214188
- Bluetooth SIG. (2023). Bluetooth Core Specification Version 5.4. Bluetooth Special Interest Group. https://www.bluetooth.com/specifications/specs/core-specification-5-4/
- Dankelmann, S. (2023). Bluetooth-LE-Spam [Repositorio GitHub]. GitHub. https://github.com/simondankelmann/Bluetooth-LE-Spam
- Microsoft. (2023, julio 14). Enabling Swift Pair in Windows 10 for Bluetooth devices. Microsoft Learn. https://learn.microsoft.com/en-us/windows-hardware/drivers/bluetooth/

## Autores:
- Jean Molina
- Marlon Freire
- Bryan Saltos
