# 🏥 Proyecto Final Ciberseguridad: Hospital General de Madrid

Este repositorio contiene el trabajo integral realizado para el proyecto final del Bootcamp de Ciberseguridad en **4Geeks Academy**. Se presenta un caso de estudio sobre el **Hospital General de Madrid** (organización ficticia), que abarca la respuesta ante incidentes, auditoría ofensiva y gobernanza técnica bajo marcos de trabajo internacionales.

## 📌 Descripción del Proyecto
El objetivo principal fue asegurar la infraestructura de un servidor crítico con la dirección IP **192.168.122.10**. Este activo custodia historiales clínicos e información sensible de pacientes y personal. El proyecto demuestra la capacidad de actuar en los tres pilares de la seguridad: detección, defensa y cumplimiento normativo (RGPD/ENS).



## 📁 Fases y Documentación

### 1. 🔍 Análisis Forense y Respuesta a Incidentes
Informe técnico sobre la identificación y contención de un compromiso real detectado en la infraestructura.

* **Vector de Intrusión:** Acceso exitoso mediante **SSH como usuario root** desde la dirección IP externa **192.168.0.134** el 08 de octubre a las 17:40:59.
* **Causa Raíz:** El atacante obtuvo la credencial mediante la lectura del archivo `wp-config.php`, expuesto por una configuración de permisos **777** y la directiva **Indexes** activa en el servidor web.
* **Análisis de Logs:** Identificación de la arquitectura **Systemd-Journald**. Se determinó que no existió borrado de logs, sino que los registros son binarios, requiriendo el uso de `journalctl` para la auditoría técnica.
* **Post-Explotación:** Detección de manipulación de privilegios mediante el uso de `visudo` y desactivación de servicios del sistema (`speech-dispatcher`) para reducir la visibilidad de la actividad maliciosa.
* **Remediación:** Cierre del acceso root en SSH (`PermitRootLogin no`), normalización de permisos (755 para directorios / 644 para ficheros) y rotación de credenciales con alta complejidad.

### 2. 🛡️ Auditoría de Pentesting (Servicio FTP)
Evaluación de seguridad de "caja gris" realizada sobre el puerto 21 para identificar vectores de fuga de información.

* **Hallazgo Principal:** Vulnerabilidad de acceso anónimo (**ftp-anon**) que permitía la entrada sin autenticación en el servicio `vsftpd 3.0.3`.
* **Prueba de Concepto (PoC):** Demostración de acceso no autorizado mediante el usuario `anonymous` y auditoría de permisos de transferencia.
* **Mitigación:** Endurecimiento del servicio mediante el cambio de la directiva `anonymous_enable` a **NO** y recomendación estratégica de migración a **SFTP** para garantizar el cifrado en tránsito.

### 3. 📜 SGSI y Marco Estratégico NIST
Manual de gestión de seguridad alineado con **ISO 27001** y el framework **NIST SP 800-61**.

* **Gobernanza de Logs:** Diseño de una arquitectura de **centralización de logs (SIEM con Wazuh)** para superar la complejidad de la auditoría local de registros binarios y garantizar la inmutabilidad de las evidencias.
* **Políticas DLP:** Restricción estricta de medios extraíbles (**USB**) mediante GPO para prevenir la exfiltración de datos personales (PII) y la entrada de ransomware.
* **Control de Identidades:** Implementación de políticas de robustez de contraseñas (mínimo 12 caracteres) y prohibición de reutilización de claves entre servicios críticos (Web, DB y Sistema).

## 🛠️ Stack Tecnológico
* **Sistemas:** Linux Debian (Kernel 6.1).
* **Servicios:** Apache2, MariaDB, vsftpd, OpenSSH.
* **Herramientas:** Journalctl, Nmap, Netstat, Grep, Find.
* **Frameworks:** NIST SP 800-61, ISO 27001, RGPD, ENS.

---

**Autor:** Arturo Martín-Vegue

**Bootcamp:** 4Geeks Academy

**Fecha:** 6 de enero de 2026

