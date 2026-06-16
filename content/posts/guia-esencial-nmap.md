---
title: "Nmap para Pentesting: Guía de Enumeración Esencial"
date: 2026-06-16
draft: false
categories: ["Pentesting"]
tags: ["nmap", "recon", "networking", "herramientas"]
---

El reconocimiento es la fase más crítica de cualquier auditoría de seguridad. No puedes atacar lo que no sabes que existe. En esta guía rápida cubriremos los comandos esenciales de **Nmap** para moverte eficientemente en tus laboratorios y exámenes (como el eJPTv2).

## 1. El Escaneo Inicial (Quick Scan)
Para no perder tiempo en redes grandes, lo ideal es lanzar un escaneo rápido para identificar qué hosts están vivos y qué puertos comunes tienen abiertos:

```bash
nmap -sT --top-ports 100 10.10.10.X

--top-ports 100: Escanea solo los 100 puertos más frecuentes.
-sT: Utiliza un escaneo TCP Connect (ideal si no tienes privilegios de root).
```

## 2. Escaneo de Versiones y Scripts
Una vez que detectas puertos abiertos, necesitas saber qué servicio corre exactamente en ellos y si hay vulnerabilidades evidentes. Para eso usamos:

```bash
nmap -sC -sV -p 22,80,443 10.10.10.X

-sV: Detecta la versión exacta del software (ej. Apache 2.4.41 en lugar de solo saber que el puerto 80 está abierto).
-sC: Ejecuta los scripts de enumeración por defecto de Nmap (NSE). Es excelente para detectar configuraciones incorrectas de forma automática.
```

## 3. Escaneo Completo de Puertos (Full Scan)
Antes de dar por terminado el reconocimiento de una máquina, debes asegurarte de revisar absolutamente todo el rango de puertos (del 1 al 65535):

```bash
nmap -p- --min-rate 5000 10.10.10.X

-p-: Escanea los 65,535 puertos.
--min-rate 5000: Envía paquetes a una velocidad mínima de 5000 por segundo (ideal para entornos controlados).
```

## 4. Guia Rápida de Parámetros

| Parámetro | ¿Qué hace? | ¿Cuándo usarlo? |
|-----------|-----------|-----------------|
| -p- | Escanea todos los puertos | Al final, para no dejar nada fuera. |
| -Pn | Omite el ping inicial | Cuando el host bloquea paquetes ICMP. |
| -oN | Guarda el output en texto plano | Siempre, para documentar tu reporte. |

`Tip`: Acostúmbrate siempre a guardar tus escaneos agregando -oN mi_escaneo.txt. En el mundo profesional, si no documentas tu output, tu trabajo no existe.