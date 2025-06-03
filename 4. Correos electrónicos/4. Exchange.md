### 📨 Elementos Recuperables y Forense en Microsoft Exchange y Microsoft 365

---

## 🔎 1. Ubicación y Adquisición de Correos

| Categoría                  | Detalle                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------- |
| **Dónde reside el correo** | Puede estar en el servidor Exchange, en la nube (O365), o localmente (PST/OST).         |
| **Tipos de adquisición**   | Imagen de disco, exportación de buzones (.PST), herramientas forenses.                  |
| **Retos**                  | Servidores críticos, acceso remoto, grandes volúmenes de datos, técnicas de compresión. |
| **Herramientas**           | EnCase, FTK, X-Ways, Aid4Mail, Mail Examiner, Emailchemy, Logikcull.                    |

---

## 💽 2. Almacenes de Exchange (.EDB/.STM/.LOG)

| Elemento   | Función                                                                                 |
| ---------- | --------------------------------------------------------------------------------------- |
| `.EDB`     | Base de datos principal desde Exchange 2007 en formato ESE. Contiene correos, adjuntos. |
| `.STM`     | Anterior a 2007. Contiene adjuntos MIME y puede contener mensajes.                      |
| `.LOG`     | Archivos de transacciones, pueden tener correos no volcados aún al .EDB.                |
| `esentutl` | Herramienta nativa de Exchange para recuperar datos desde los logs.                     |

---

## 📁 3. Recoverable Items (Elementos Recuperables)

| Subcarpeta           | Función                                                                      |
| -------------------- | ---------------------------------------------------------------------------- |
| **Deletions**        | Correo eliminado de "Elementos eliminados" o con Shift+Delete (Soft delete). |
| **Purges**           | Correos movidos desde Deletions por tiempo de retención.                     |
| **Versions**         | Copias en escritura de elementos modificados.                                |
| **Audits**           | Registros si la auditoría de buzones está activa (90 días por defecto).      |
| **Calendar Logging** | Cambios en calendarios cuando el registro está activo.                       |
| **DiscoveryHolds**   | Elementos retenidos por litigios (Litigation/InPlace Hold).                  |

**Notas clave:**

* Residen en el subárbol no IPM.
* Indexado para búsquedas eDiscovery.
* Tiempo de retención por defecto: 14 días (elementos) y 30 días (buzones eliminados).

---

## 🧰 4. Técnicas de Exportación

| Método                          | Detalle                                                                                   |
| ------------------------------- | ----------------------------------------------------------------------------------------- |
| **WSB (Windows Server Backup)** | Copias .VHD con datos de Exchange, incluye volumen shadow copy.                           |
| **PowerShell Cmdlets**          | `New-MailboxExportRequest`, `New-MailboxImportRequest`. Filtrado por asunto, fecha, etc.  |
| **ExMerge (Legacy)**            | Herramienta antigua para Exchange 2003 y anteriores. Exporta buzones individuales a .PST. |

---

## 🔍 5. eDiscovery y Búsqueda de Cumplimiento

| Categoría               | Detalle                                                                                  |
| ----------------------- | ---------------------------------------------------------------------------------------- |
| **Compliance Search**   | Búsqueda avanzada en múltiples buzones (hasta 500 buzones o 50 GB por búsqueda).         |
| **Filtros disponibles** | Por cuerpo, asunto, remitente, destinatario, adjuntos, fechas, etc.                      |
| **Limitaciones**        | No se indexan adjuntos cifrados o no reconocidos.                                        |
| **Litigation Hold**     | Evita borrado de mensajes seleccionados o buzones enteros, incluso para correos futuros. |

---

## 📤 6. Microsoft 365: Exportaciones y Búsqueda

| Función                | Detalle                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------ |
| **Content Search**     | Busca en toda la organización sin límite de buzones.                                 |
| **Exportación a .PST** | Hasta 2 TB por búsqueda. Se divide en archivos de 10 GB.                             |
| **Límites**            | 10 exportaciones activas máximo. Se requiere pertenecer al grupo eDiscovery Manager. |
| **Velocidad**          | 100 buzones ≈ 30 seg. / 100.000 buzones ≈ 25 min.                                    |
| **Auditoría M365**     | Permite rastrear actividad de usuarios/atacantes.                                    |

---

### ✅ Recomendaciones Finales

* Siempre adquirir también los `.LOG` y `.STM` (si aplica).
* Aprovechar las capacidades de filtrado de PowerShell para reducir volumen de análisis.
* Usar retenciones legales (Litigation Hold) para preservar evidencia sin intervención del usuario.
* Apoyarse en herramientas Exchange-aware para garantizar la consistencia de datos.

---

**Referencias útiles:**

* [Recoverable Items Folder](https://learn.microsoft.com/en-us/exchange/security-and-compliance/recoverable-itemsfolder/)
* [Mailbox Audit Logging](https://learn.microsoft.com/en-us/exchange/policy-and-compliance/mailbox-auditlogging/mailbox-audit-logging)
* [PowerShell Export Commands](https://learn.microsoft.com/en-us/powershell/module/exchange/newmailboxexportrequest)
* [Content Search in M365](https://learn.microsoft.com/en-us/microsoft-365/compliance/content-search)
