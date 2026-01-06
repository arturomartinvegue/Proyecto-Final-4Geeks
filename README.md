# Proyecto Final Ciberseguridad: Hospital General de Madrid

Este repositorio contiene el trabajo realizado para el proyecto final del Bootcamp de Ciberseguridad en **4Geeks Academy**. Se presenta un caso de estudio integral sobre el **Hospital General de Madrid** (organización ficticia), cubriendo la respuesta a incidentes, auditoría ofensiva y gobernanza técnica.

## 📌 Descripción del Proyecto
El objetivo principal fue asegurar la infraestructura de un servidor crítico (IP `192.168.122.10`) que custodia historiales clínicos y servicios administrativos. El proyecto demuestra la capacidad de actuar en los tres pilares de la seguridad: detección, defensa y cumplimiento.

---

## 📁 Fases y Documentación

### 1. [Análisis Forense y Respuesta a Incidentes](./01_Informe-Forense-Hospital.pdf)
Informe técnico detallado sobre la contención de un compromiso real detectado en el servidor.
* **Vector de ataque:** Explotación de credenciales débiles (`debian/123456`) y configuraciones por defecto.
* **Análisis Forense:** Identificación de técnicas anti-forenses, específicamente el borrado de registros de sistema (`auth.log` y `syslog`) por parte del atacante.
* **Remediación:** Normalización de permisos en el webroot (755/644), hardening del servicio SSH y rotación de credenciales de base de datos bajo estándares de alta complejidad.

### 2. [Auditoría de Pentesting (Servicio FTP)](./02_Pentesting-FTP-Vulnerability.pdf)
Evaluación de seguridad de caja gris para identificar vectores de fuga de información.
* **Hallazgo principal:** Vulnerabilidad de acceso anónimo (`ftp-anon`) en el puerto 21.
* **Prueba de Concepto (PoC):** Demostración de acceso no autorizado y auditoría de permisos de escritura.
* **Mitigación:** Configuración del servicio `vsftpd` para restringir el acceso y recomendación estratégica de migración a SFTP para garantizar el cifrado en tránsito.

### 3. [SGSI y Marco Estratégico NIST](./03_SGSI-NIST-Framework-Plan.pdf)
Manual de gestión de seguridad alineado con **ISO 27001** y el framework **NIST SP 800-61**.
* **Políticas DLP:** Restricción estricta de medios extraíbles (USB) mediante GPO para prevenir exfiltración de datos y entrada de ransomware.
* **Gobernanza:** Clasificación de activos (especialmente historiales médicos/RGPD) y diseño de una arquitectura de centralización de logs (SIEM) para garantizar la inmutabilidad de las evidencias.
* **Control de Identidades:** Implementación de políticas de robustez de contraseñas (mínimo 12 caracteres) y prohibición de cuentas genéricas.

---

## 🛠️ Stack Tecnológico
* **Sistemas:** Linux Debian (Kernel 6.1).
* **Servicios:** Apache2, MariaDB, vsftpd, OpenSSH.
* **Herramientas:** Nmap, Netstat, Grep, Find.
* **Marcos de trabajo:** NIST, ISO 27001, RGPD.

---
**Autor:** Arturo Martín-Vegue  
**Bootcamp:** 4Geeks Academy  
**Fecha:** 6 de enero de 2026
