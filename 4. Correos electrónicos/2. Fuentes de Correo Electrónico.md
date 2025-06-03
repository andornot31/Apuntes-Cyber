### Fuentes principales de correo electrónico en Windows:

#### 1. Microsoft Outlook (PST y OST)
* **PST**: Almacena correos, contactos y calendarios.
	* Ruta típica:
		* WinXP: `%USERPROFILE%\Local Settings\Application Data\Microsoft\Outlook`
		* Win7+: `%USERPROFILE%\AppData\Local\Microsoft\Outlook`
	* Tamaño máx.: 50 GB
	* Herramientas: **Kernel PST Viewer**, **Photorec** (recuperación)

* **OST**: Se usa con cuentas IMAP o Exchange.
	* Misma ruta y límite que PST
	* Almacena los últimos 12 meses por defecto
	* Herramientas: **Kernel OST Viewer**, herramientas de recuperación de OST

* **Adjuntos en Outlook**:
	* Rutas temporales:
		* IE10: `%APPDATA%\Local\Microsoft\Windows\Temporary Internet Files\Content.Outlook`
		* IE11+: `%APPDATA%\Local\Microsoft\InetCache\Content.Outlook`

---

#### 2. Thunderbird (MBOX)
* Almacena correos en ficheros `.mbox`
	* Ruta: `\Users\%USERNAME%\AppData\Roaming\Thunderbird\Profiles`
	* Análisis con **Autopsy** + módulo **Email Parser** (también compatible con PST y OST)

---

#### 3. Windows 10 Mail App
* Correos en HTML o texto con extensión `.dat`
	* Ruta: `\Users\{user_name}\AppData\Local\Comms\Unistore\data\3\`
	* Metadatos y contactos: `\Users\{user_name}\AppData\Local\Comms\UnistoreDB\store.vol` (convertir a .EDB para ver en **ViewEse**)

---

#### 4. Google (Takeout y Vault)
* **Takeout**: Exporta todo el correo en un archivo `.mbox`
	* URL: [https://takeout.google.com](https://takeout.google.com)

* **Vault**: Para cuentas GSuite (permite búsquedas, exportación con hash MD5)

* **Modo Confidencial** de Gmail puede restringir búsquedas vía API, pero no en Vault

* **Modificación de correos Gmail con Outlook**:
	* Si se usa IMAP, es posible editar y guardar mensajes
	* Pistas de manipulación:
		* Cabecera **UID** anómala
		* Cambio en campo **X-Mailer**
		* Añadido de delimitador MIME con marca temporal

---

#### 5. Microsoft Exchange Server
* Almacena todo en archivos `.EDB`
	* Rutas según versión (Exchange 2010 a 2019)
		* Versión de Exchange 2010:
		`C:\Program Files\Microsoft\Exchange Server\V14\Mailbox Database\Mailbox Database.edb`
		* Versión de Exchange Server 2013:
		`C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox database Name\Mailbox database Name.edb`
		* Versión de Exchange Server 2019 and 2016:
		`C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database Name.edb`
	* Soporta recuperación desde la carpeta “Recoverable Items” (hasta 14 días)
	* Métodos de análisis:
	    * Imagen forense
	    * **Windows Server Backup** (genera VHDs)
	    * Exportar buzones a **PST** (https://docs.microsoft.com/es-es/exchange/recipients/mailbox-import-and-export/export-procedures?view=exchserver-2019)

---

#### 6. Office365
* Acceso desde la nube a Outlook y otras apps de Office
* Herramienta **eDiscovery** permite búsquedas en:
	* Buzones de Exchange Online
	* OneDrive, SharePoint, Teams, Skype Empresarial, Yammer
- Los resultados pueden exportarse en formato **PST**.
- **30 días** de retención por defecto tras eliminar contenido.