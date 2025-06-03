### Forense de Correos Electrónicos - Resumen de Campos Clave

|**Campo**|**Descripción Resumida**|**Utilidad Forense**|**Dónde Encontrarlo / Herramientas**|
|---|---|---|---|
|**Cabecera del Email**|Contiene metadatos del mensaje como fechas, remitente, destinatario, IP, etc.|Determina origen, ruta, timestamps y cliente de correo.|Cabecera completa en cliente de correo, [MXToolbox](https://mxtoolbox.com/EmailHeaders.aspx).|
|**Message-ID**|Identificador único generado por el servidor emisor.|Trazabilidad de conversaciones, detección de spoofing.|Campo `Message-ID:` en cabecera.|
|**MAPI Headers**|Cabeceras específicas de Outlook/Exchange, como flags, IDs y timestamps locales.|Identificación de acciones del usuario (leer, reenviar, etc.), y estructura de mensajes.|Herramienta `MFCMAPI`.|
|**Content-Length**|Tamaño en bytes del cuerpo del mensaje.|Detectar modificaciones, validar integridad del mensaje.|Campo MIME del mensaje.|
|**IMAP Internal Date**|Fecha en la que el mensaje fue almacenado en el servidor IMAP.|Contrastar con fecha real de envío, detectar manipulaciones.|Registros IMAP o comandos FETCH.|
|**DKIM**|Firma digital que verifica que el contenido no ha sido alterado y proviene del dominio legítimo.|Verificar integridad y autenticidad del mensaje.|Campo `DKIM-Signature`, herramientas: [dkimvalidator.com](https://dkimvalidator.com/).|
|**SPF**|Verifica si la IP emisora está autorizada para enviar en nombre del dominio.|Detectar suplantación de dominio (spoofing).|Cabecera `Received-SPF`, DNS (TXT SPF).|
|**DMARC**|Política de autenticación que combina DKIM y SPF para decidir qué hacer ante fallos.|Determina acciones ante correos falsificados.|Registro DNS `_dmarc`, valores: `none`, `quarantine`, `reject`.|
|**Authentication Results**|Resumen del resultado de DKIM, SPF y DMARC evaluado por el servidor receptor.|Confirmar autenticidad final del mensaje.|Cabecera `Authentication-Results`. Valores: `pass`, `fail`, `neutral`, etc.|

---

### Preguntas que puede responder el análisis forense de emails

|**Pregunta**|**Datos a analizar**|
|---|---|
|¿Quién envió el email?|Dirección del remitente, IP, Message-ID, cabeceras.|
|¿Cuándo fue enviado?|Timestamps del header, IMAP Internal Date.|
|¿Desde dónde?|IP pública, dominio SMTP, geolocalización.|
|¿Es legítimo?|DKIM, SPF, DMARC, Authentication Results.|
|¿Es relevante el contenido?|Cuerpo, adjuntos, conversaciones, calendarios.|
