# Apuntes de Redes de Datos — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Crear 10 archivos `.tex` de apuntes teóricos profundos sobre redes de datos, organizados por capa OSI, con emojis, diagramas TikZ, ejemplos simples y protocolos modernos (QUIC, HTTP/3, gRPC, BBR, WireGuard).

**Architecture:** Un archivo raíz `ApuntesRedes.tex` que une todos los capítulos con `\input{}`. Cada capítulo es un `.tex` independiente en `chapters/`. Se compila con LuaLaTeX (necesario para el paquete `emoji`). Commit + push al terminar cada capítulo.

**Tech Stack:** LuaLaTeX, paquetes: `emoji`, `tcolorbox`, `tikz`, `listings`, `babel{spanish}`, `fontawesome5`, `geometry`, `hyperref`, `inputenc{utf8}`

---

## Archivo map

| Archivo | Responsabilidad |
|---|---|
| `ApuntesRedes.tex` | Raíz: portada, ToC, `\input{}` de todos los capítulos |
| `chapters/00_intro.tex` | Historia de redes, OSI vs TCP/IP, RFCs, organismos |
| `chapters/01_capa1_fisica.tex` | Cables UTP, fibra, normas EIA/TIA, Wi-Fi |
| `chapters/02_capa2_enlace.tex` | MAC, Ethernet, switch, VLAN, STP, EtherChannel |
| `chapters/03_capa3_red.tex` | IP, subnetting, routing, IPv6, NAT, BGP |
| `chapters/04_capa4_transporte.tex` | TCP, UDP, handshake, flags, control de congestión |
| `chapters/05_capa5_sesion.tex` | SSH, sesiones TLS, NetBIOS |
| `chapters/06_capa6_presentacion.tex` | Codificación, cifrado, TLS/SSL, Protobuf |
| `chapters/07_capa7_aplicacion.tex` | DHCP, DNS, HTTP/1.1–3, SMTP, FTP, firewall |
| `chapters/08_modernos_google.tex` | QUIC, HTTP/3, gRPC, BBR, DoH, WebRTC, Wi-Fi 7 |
| `chapters/09_seguridad_redes.tex` | VPN, WireGuard, mTLS, Zero Trust, ataques, RPKI |

---

## Task 0: Setup — estructura base y `ApuntesRedes.tex`

**Files:**
- Create: `ApuntesRedes.tex`
- Create: `chapters/` (directorio vacío con `.gitkeep`)

- [ ] **Step 1: Crear `ApuntesRedes.tex`**

```latex
% ApuntesRedes.tex — Archivo raíz
\documentclass[12pt, a4paper]{book}

% Encoding & Language
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[spanish]{babel}

% Emojis (requiere LuaLaTeX)
\usepackage{emoji}
\setemojifont{Noto Color Emoji}

% Iconos extra
\usepackage{fontawesome5}

% Layout
\usepackage[top=2.5cm, bottom=2.5cm, left=3cm, right=3cm]{geometry}
\usepackage{hyperref}
\hypersetup{
    colorlinks=true,
    linkcolor=blue!70!black,
    urlcolor=blue!70!black,
    pdftitle={Apuntes de Redes de Datos},
    pdfauthor={Aldo Zepeda}
}

% Cajas visuales
\usepackage[most]{tcolorbox}
\tcbuselibrary{skins, breakable}

% Cajas personalizadas
\newtcolorbox{concepto}[1][]{
    title={\emoji{brain} Concepto},
    colback=blue!8!white, colframe=blue!50!black,
    fonttitle=\bfseries, breakable, #1
}
\newtcolorbox{ejemplo}[1][]{
    title={\emoji{package} Ejemplo real},
    colback=green!8!white, colframe=green!50!black,
    fonttitle=\bfseries, breakable, #1
}
\newtcolorbox{cuidado}[1][]{
    title={\emoji{warning} Cuidado},
    colback=orange!15!white, colframe=orange!70!black,
    fonttitle=\bfseries, breakable, #1
}
\newtcolorbox{moderno}[1][]{
    title={\emoji{rocket} Tecnología Moderna},
    colback=violet!8!white, colframe=violet!60!black,
    fonttitle=\bfseries, breakable, #1
}
\newtcolorbox{codigo}[1][]{
    title={\emoji{laptop} Configuración / Código},
    colback=gray!10!white, colframe=gray!60!black,
    fonttitle=\bfseries, breakable, #1
}

% Código fuente
\usepackage{listings}
\lstset{
    basicstyle=\ttfamily\small,
    backgroundcolor=\color{gray!10},
    frame=single,
    breaklines=true,
    inputencoding=utf8,
    extendedchars=true
}

% Diagramas
\usepackage{tikz}
\usetikzlibrary{shapes, arrows, positioning, calc, decorations.pathreplacing}

% Matemáticas
\usepackage{amsmath}

% Colores
\usepackage{xcolor}

% Tablas
\usepackage{booktabs}
\usepackage{multirow}

% Gráficos
\usepackage{graphicx}
\graphicspath{{assets/}}

%% ============================================================
\begin{document}

% Portada
\begin{titlepage}
    \centering
    \vspace*{2cm}
    {\Huge\bfseries \emoji{globe-showing-americas} Apuntes de Redes de Datos\par}
    \vspace{0.5cm}
    {\Large\bfseries Redes de Datos Seguras\par}
    \vspace{1cm}
    {\large Basado en MADO-31 — UNAM Facultad de Ingeniería\par}
    \vspace{0.5cm}
    {\large Aldo Zepeda Moctezuma\par}
    \vspace{0.5cm}
    {\normalsize \today\par}
    \vspace{2cm}
    {\large\itshape ``Si no puedes explicarlo simplemente, no lo entiendes suficientemente bien.'' \\ --- Albert Einstein\par}
\end{titlepage}

\tableofcontents
\newpage

% Capítulos
\input{chapters/00_intro}
\input{chapters/01_capa1_fisica}
\input{chapters/02_capa2_enlace}
\input{chapters/03_capa3_red}
\input{chapters/04_capa4_transporte}
\input{chapters/05_capa5_sesion}
\input{chapters/06_capa6_presentacion}
\input{chapters/07_capa7_aplicacion}
\input{chapters/08_modernos_google}
\input{chapters/09_seguridad_redes}

\end{document}
```

- [ ] **Step 2: Crear directorio `chapters/` con placeholder**

```bash
mkdir -p "D:/Codigo Abierto/RedesDeDatos/chapters"
mkdir -p "D:/Codigo Abierto/RedesDeDatos/assets"
# Crear archivos .tex vacíos para que compile desde el inicio
for f in 00_intro 01_capa1_fisica 02_capa2_enlace 03_capa3_red \
          04_capa4_transporte 05_capa5_sesion 06_capa6_presentacion \
          07_capa7_aplicacion 08_modernos_google 09_seguridad_redes; do
  echo "% TODO" > "D:/Codigo Abierto/RedesDeDatos/chapters/${f}.tex"
done
```

- [ ] **Step 3: Verificar que compila (aunque esté vacío)**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -E "^!" | head -20
```
Esperado: sin líneas `!` (errores). PDF generado aunque vacío.

- [ ] **Step 4: Commit**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add ApuntesRedes.tex chapters/ assets/
git commit -m "chore: estructura base LaTeX con portada y paquetes"
git push
```

---

## Task 1: `00_intro.tex` — Introducción y modelos OSI/TCP-IP

**Files:**
- Modify: `chapters/00_intro.tex`

- [ ] **Step 1: Escribir el capítulo**

Contenido mínimo requerido con este esqueleto exacto:

```latex
\chapter{\emoji{globe-showing-americas} Introducción a las Redes de Datos}

%% ── 1.1 ¿Qué es una red? ──────────────────────────────────────────────────
\section{\emoji{thinking-face} ¿Qué es una red de datos?}

\begin{concepto}
Una \textbf{red de datos} es un conjunto de dispositivos (computadoras, teléfonos,
impresoras) conectados entre sí para poder \textbf{compartir información}.

\emoji{light-bulb} \textbf{Analogía:} Imagina que tienes amigos en diferentes casas.
Una red es como un sistema de tuberías que conecta todas las casas para que
puedan mandarse agua (datos) entre sí.
\end{concepto}

%% ── 1.2 Historia breve ────────────────────────────────────────────────────
\section{\emoji{books} Un poco de historia}

\begin{itemize}
    \item \textbf{1969 — ARPANET:} La primera red de computadoras del mundo.
          Solo 4 nodos: UCLA, Stanford, UCSB y University of Utah.
          \emoji{exploding-head} ¡El primer mensaje enviado fue ``lo'' porque el
          sistema crasheó antes de terminar ``login''!
    \item \textbf{1983 — Nacimiento del Internet:} ARPANET adopta TCP/IP.
    \item \textbf{1991 — World Wide Web:} Tim Berners-Lee inventa HTTP y HTML.
    \item \textbf{2021 — QUIC (RFC 9000):} Google revoluciona el transporte web.
          Hoy el 25\% del tráfico de Internet usa QUIC.
\end{itemize}

%% ── 1.3 Modelo OSI ────────────────────────────────────────────────────────
\section{\emoji{layer-cake} El Modelo OSI — Las 7 Capas}

\begin{concepto}
El \textbf{modelo OSI} (Open Systems Interconnection) es un modelo de referencia
creado por ISO en 1984. Divide la comunicación en red en \textbf{7 capas},
cada una con una responsabilidad específica.

\emoji{light-bulb} \textbf{Analogía:} Es como enviar una carta por correo:
escribes el mensaje (capa 7), lo metes en un sobre (capa 6), le pones dirección
(capas 3-4), el cartero lo lleva (capas 1-2). Cada capa hace su parte sin
saber qué hacen las demás.
\end{concepto}

\begin{center}
\begin{tikzpicture}[
    layer/.style={rectangle, draw, minimum width=8cm, minimum height=0.8cm,
                  font=\bfseries\small, align=center},
    app/.style={layer, fill=red!20},
    pres/.style={layer, fill=orange!20},
    ses/.style={layer, fill=yellow!20},
    trans/.style={layer, fill=green!20},
    net/.style={layer, fill=cyan!20},
    link/.style={layer, fill=blue!20},
    phys/.style={layer, fill=purple!20}
]
\node[app]  (L7) at (0,4.8) {Capa 7 — Aplicación (Application)};
\node[pres] (L6) at (0,4.0) {Capa 6 — Presentación (Presentation)};
\node[ses]  (L5) at (0,3.2) {Capa 5 — Sesión (Session)};
\node[trans](L4) at (0,2.4) {Capa 4 — Transporte (Transport)};
\node[net]  (L3) at (0,1.6) {Capa 3 — Red (Network)};
\node[link] (L2) at (0,0.8) {Capa 2 — Enlace de Datos (Data Link)};
\node[phys] (L1) at (0,0.0) {Capa 1 — Física (Physical)};
\end{tikzpicture}
\end{center}

\begin{table}[h!]
\centering
\begin{tabular}{clll}
\toprule
\textbf{Capa} & \textbf{Nombre} & \textbf{¿Qué hace?} & \textbf{Ejemplos} \\
\midrule
7 & Aplicación  & Interfaz con el usuario          & HTTP, DNS, SMTP, FTP \\
6 & Presentación & Codifica y cifra datos           & TLS, Base64, JPEG \\
5 & Sesión      & Gestiona sesiones                & SSH, NetBIOS, RPC \\
4 & Transporte  & Entrega confiable extremo-a-extremo & TCP, UDP, QUIC \\
3 & Red         & Enrutamiento entre redes         & IP, ICMP, OSPF, BGP \\
2 & Enlace      & Entrega en la misma red local    & Ethernet, MAC, ARP \\
1 & Física      & Bits sobre el cable              & UTP, Fibra, Wi-Fi \\
\bottomrule
\end{tabular}
\caption{Resumen del modelo OSI}
\end{table}

\begin{cuidado}
\textbf{Mnemónica para recordar las capas (de arriba a abajo):}\\
\textbf{A}ll \textbf{P}eople \textbf{S}eem \textbf{T}o \textbf{N}eed \textbf{D}ata \textbf{P}rocessing\\
(Application, Presentation, Session, Transport, Network, Data Link, Physical)
\end{cuidado}

%% ── 1.4 Modelo TCP/IP ─────────────────────────────────────────────────────
\section{\emoji{computer} El Modelo TCP/IP (Modelo de Internet)}

\begin{concepto}
El \textbf{modelo TCP/IP} es el que usa Internet en la vida real. Tiene solo
\textbf{4 capas} (agrupa las 7 de OSI). Fue creado por DARPA en los 70s.
\end{concepto}

\begin{center}
\begin{tikzpicture}[
    layer/.style={rectangle, draw, minimum width=8cm, minimum height=0.9cm,
                  font=\bfseries\small, align=center}
]
\node[layer, fill=red!20]    at (0,2.7) {Aplicación (capas OSI 5+6+7)};
\node[layer, fill=green!20]  at (0,1.8) {Transporte — TCP / UDP (capa OSI 4)};
\node[layer, fill=cyan!20]   at (0,0.9) {Internet — IP (capa OSI 3)};
\node[layer, fill=purple!20] at (0,0.0) {Acceso a la red (capas OSI 1+2)};
\end{tikzpicture}
\end{center}

%% ── 1.5 PDUs ──────────────────────────────────────────────────────────────
\section{\emoji{package} PDUs — ¿Cómo se llaman los datos en cada capa?}

Cada capa tiene un nombre especial para los datos que maneja:

\begin{table}[h!]
\centering
\begin{tabular}{cll}
\toprule
\textbf{Capa OSI} & \textbf{PDU} & \textbf{Analogía} \\
\midrule
7-5 & Datos (Data)    & El mensaje que escribiste \\
4   & Segmento (TCP) / Datagrama (UDP) & El sobre con dirección del destinatario \\
3   & Paquete (Packet) & La caja de envío con dirección IP \\
2   & Trama (Frame)    & El camión que lleva la caja \\
1   & Bits             & Las ruedas girando \\
\bottomrule
\end{tabular}
\end{table}

%% ── 1.6 RFC e IETF ────────────────────────────────────────────────────────
\section{\emoji{scroll} RFCs — Las reglas de Internet}

\begin{concepto}
Un \textbf{RFC} (Request for Comments) es un documento técnico que define cómo
funciona un protocolo de Internet. Son publicados por el \textbf{IETF}
(Internet Engineering Task Force).

\emoji{light-bulb} \textbf{Analogía:} Los RFCs son como las reglas del fútbol.
Todos los equipos (fabricantes, desarrolladores) deben seguirlas para poder
jugar juntos.
\end{concepto}

RFCs importantes que verás en estos apuntes:
\begin{itemize}
    \item \textbf{RFC 791} — IPv4 (1981)
    \item \textbf{RFC 793} — TCP (1981)
    \item \textbf{RFC 768} — UDP (1980)
    \item \textbf{RFC 8446} — TLS 1.3 (2018)
    \item \textbf{RFC 9000} — QUIC (2021)
    \item \textbf{RFC 9114} — HTTP/3 (2022)
\end{itemize}

Organismos de estandarización:
\begin{itemize}
    \item \textbf{IETF} — Define protocolos de Internet (RFCs)
    \item \textbf{IEEE} — Estándares de hardware: Ethernet (802.3), Wi-Fi (802.11)
    \item \textbf{ISO} — Modelo OSI, ISO 27000 (seguridad)
    \item \textbf{IANA} — Administra IPs, puertos y nombres de dominio globalmente
    \item \textbf{ANSI/TIA/EIA} — Estándares de cableado físico
\end{itemize}
```

- [ ] **Step 2: Compilar y verificar**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```
Esperado: `0` (cero errores).

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/00_intro.tex
git commit -m "docs: cap 0 - intro, modelos OSI y TCP/IP, RFCs"
git push
```

---

## Task 2: `01_capa1_fisica.tex` — Capa Física

**Files:**
- Modify: `chapters/01_capa1_fisica.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{electric-plug} Capa 1 — Física (Physical Layer)}

\section{\emoji{thinking-face} ¿Qué hace la capa física?}

\begin{concepto}
La \textbf{capa física} se encarga de transmitir \textbf{bits crudos} (ceros y unos)
sobre un medio físico: cable de cobre, fibra óptica o señales de radio.

\emoji{light-bulb} \textbf{Analogía:} Es como el sistema eléctrico de tu casa.
No sabe qué aparato vas a enchufar ni para qué lo usas. Solo asegura que
la electricidad llegue correctamente.
\end{concepto}

\section{\emoji{thread} Cable UTP — Unshielded Twisted Pair}

\begin{concepto}
\textbf{UTP} (par trenzado no blindado) es el cable más común en redes LAN.
Tiene 4 pares de hilos de cobre, cada par \textbf{trenzado} entre sí.

\emoji{light-bulb} \textbf{¿Por qué trenzado?} Al trenzar los cables se cancelan
las interferencias electromagnéticas entre sí (cancelación de interferencia
por inducción mutua). Sin el trenzado, las señales se mezclarían como
radios que se solapan.
\end{concepto}

\subsection{Categorías de cable UTP}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
\textbf{Categoría} & \textbf{Velocidad máx.} & \textbf{Distancia} & \textbf{Uso típico} \\
\midrule
Cat 5e  & 1 Gbps     & 100 m & Redes de hogar/oficina \\
Cat 6   & 10 Gbps    & 55 m  & Redes corporativas \\
Cat 6a  & 10 Gbps    & 100 m & Data centers \\
Cat 7   & 10 Gbps    & 100 m & Apantallado (STP), industrial \\
Cat 8   & 40 Gbps    & 30 m  & Conexiones cortas en data center \\
\bottomrule
\end{tabular}
\caption{Categorías de cable UTP}
\end{table}

\begin{cuidado}
La categoría del cable determina su máxima velocidad. Usar Cat 5e en una
red de 10 Gbps hará que el switch negocie automáticamente a 1 Gbps.
\textbf{El eslabón más lento limita toda la cadena.}
\end{cuidado}

\subsection{Normas T568-A y T568-B}

\begin{concepto}
Las normas \textbf{ANSI/EIA/TIA T568-A} y \textbf{T568-B} definen el orden
de los 8 hilos dentro del conector RJ-45.
\end{concepto}

\begin{center}
\begin{tikzpicture}[pin/.style={rectangle, draw, minimum width=0.5cm,
                                minimum height=1.2cm, font=\tiny}]
% T568-B pin order
\node[font=\bfseries] at (2, 1.8) {T568-B (más común en México)};
\foreach \col/\name/\i in {
    white!70!orange/BL-N/1,
    orange/N/2,
    white!70!green/BL-V/3,
    blue/AZ/4,
    white!70!blue/BL-AZ/5,
    green/V/6,
    white!70!brown/BL-C/7,
    brown/C/8
}{
    \node[pin, fill=\col] at (\i*0.6 - 0.3, 0.6) {};
    \node[font=\tiny] at (\i*0.6 - 0.3, -0.1) {\i};
}
\end{tikzpicture}
\end{center}

Orden T568-B: \texttt{BL-N, N, BL-V, AZ, BL-AZ, V, BL-C, C}
(Blanco-Naranja, Naranja, Blanco-Verde, Azul, Blanco-Azul, Verde, Blanco-Café, Café)

\begin{ejemplo}
\textbf{Cable straight-through (conexión directa):}
Ambos extremos usan T568-B. Se usa para conectar:
\begin{itemize}
    \item PC \textrightarrow{} Switch
    \item Switch \textrightarrow{} Router
\end{itemize}

\textbf{Cable crossover (cruzado):}
Un extremo T568-A, el otro T568-B. Los pares de TX/RX se invierten.
Hoy en día casi no se necesita porque los switches modernos tienen
\textbf{Auto-MDI/MDIX} (detectan y cruzan automáticamente).
\end{ejemplo}

\section{\emoji{optical-disk} Fibra Óptica}

\begin{concepto}
En lugar de electricidad, la fibra usa \textbf{pulsos de luz} para transmitir datos.
Inmune a interferencias electromagnéticas, puede llegar a \textbf{kilómetros}
sin pérdida de señal.

\emoji{light-bulb} \textbf{Analogía:} Si el cable UTP es como hablar por teléfono
de lata con hilo, la fibra es como usar un láser para mandar mensajes
a través de un espejo muy largo.
\end{concepto}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
 & \textbf{Multimodo (MMF)} & \textbf{Monomodo (SMF)} \\
\midrule
Núcleo   & 50–62.5 µm & 8–10 µm \\
Distancia & hasta 550 m & hasta 100 km \\
Costo    & Menor & Mayor \\
Luz      & LED / VCSEL & Láser diodo \\
Uso      & Dentro de edificios & Entre ciudades / ISP \\
Color del conector & Naranja / Aqua & Amarillo \\
\bottomrule
\end{tabular}
\caption{Multimodo vs Monomodo}
\end{table}

\section{\emoji{wireless} Wi-Fi — Estándares IEEE 802.11}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
\textbf{Estándar} & \textbf{Nombre común} & \textbf{Frec.} & \textbf{Velocidad máx.} \\
\midrule
802.11b  & Wi-Fi 1 & 2.4 GHz & 11 Mbps \\
802.11g  & Wi-Fi 3 & 2.4 GHz & 54 Mbps \\
802.11n  & Wi-Fi 4 & 2.4/5 GHz & 600 Mbps \\
802.11ac & Wi-Fi 5 & 5 GHz & 3.5 Gbps \\
802.11ax & Wi-Fi 6/6E & 2.4/5/6 GHz & 9.6 Gbps \\
802.11be & \textbf{Wi-Fi 7} & 2.4/5/6 GHz & \textbf{46 Gbps} \\
\bottomrule
\end{tabular}
\caption{Evolución de Wi-Fi}
\end{table}

\begin{moderno}
\textbf{Wi-Fi 7 (802.11be, 2024)} introduce \textbf{Multi-Link Operation (MLO)}:
un dispositivo puede transmitir en múltiples bandas \textit{simultáneamente}
(por ejemplo, 5 GHz y 6 GHz al mismo tiempo), reduciendo latencia y
aumentando throughput. Clave para gaming y realidad virtual.
\end{moderno}

\section{\emoji{toolbox} Cableado Estructurado}

\begin{concepto}
Un sistema de \textbf{cableado estructurado} es la infraestructura de cables
y componentes instalada en un edificio de forma organizada y estándar,
diseñada para durar décadas y soportar cualquier tecnología futura.
\end{concepto}

Los 6 subsistemas (norma ANSI/EIA/TIA 568):
\begin{enumerate}
    \item \textbf{Cableado horizontal} — del armario de telecomunicaciones al área de trabajo
    \item \textbf{Área de trabajo} — jacks RJ-45 en la pared, patch cords
    \item \textbf{Armario de telecomunicaciones} — patch panels, switches
    \item \textbf{Cableado backbone (vertical)} — entre pisos del edificio
    \item \textbf{Sala de equipos} — servidores, routers principales
    \item \textbf{Entrada de servicios} — donde llega el ISP al edificio
\end{enumerate}
```

- [ ] **Step 2: Compilar**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```
Esperado: `0`

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/01_capa1_fisica.tex
git commit -m "docs: cap 1 - capa física, UTP, fibra, Wi-Fi 7, cableado estructurado"
git push
```

---

## Task 3: `02_capa2_enlace.tex` — Capa de Enlace de Datos

**Files:**
- Modify: `chapters/02_capa2_enlace.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{link} Capa 2 — Enlace de Datos (Data Link Layer)}

\section{\emoji{thinking-face} ¿Qué hace la capa de enlace?}

\begin{concepto}
La capa de enlace mueve \textbf{tramas (frames)} entre dos dispositivos
\textit{directamente conectados} en la misma red local (LAN).
Usa \textbf{direcciones MAC} en lugar de IPs.

\emoji{light-bulb} \textbf{Analogía:} Si las IPs son como las direcciones postales
de casas en cualquier ciudad del mundo, las MACs son como el número de asiento
en un salón de clases: solo funcionan dentro del salón.
\end{concepto}

\section{\emoji{id-button} Dirección MAC}

\begin{concepto}
La \textbf{dirección MAC} (Media Access Control) es un identificador de 48 bits
(6 bytes) grabado en la tarjeta de red (NIC) de fábrica. Es única en el mundo.

Formato: \texttt{AA:BB:CC:DD:EE:FF} (hexadecimal, separado por ``:'' o ``-'')
\end{concepto}

\begin{verbatim}
  MAC: 00:1A:2B:3C:4D:5E
       └──────┘ └────────┘
          OUI     NIC-specific
   (fabricante)   (único del dispositivo)
\end{verbatim}

Los primeros 3 bytes son el \textbf{OUI} (Organizationally Unique Identifier):
identifica al fabricante. Por ejemplo, \texttt{00:1A:2B} = Cisco.

\section{\emoji{incoming-envelope} ARP — Address Resolution Protocol}

\begin{concepto}
\textbf{ARP} traduce direcciones IP a direcciones MAC. Necesario porque la
capa de enlace solo entiende MACs, pero nosotros configuramos IPs.

\emoji{light-bulb} \textbf{Analogía:} Sabes el nombre de tu compañero (IP) pero
necesitas saber en qué asiento está (MAC). ARP es como gritar
``¡Oye, Juan! ¿dónde estás sentado?'' y esperar que Juan responda.
\end{concepto}

Proceso ARP:
\begin{enumerate}
    \item PC-A quiere hablar con \texttt{192.168.1.5} pero no sabe su MAC
    \item PC-A envía \textbf{ARP Request} en broadcast (\texttt{FF:FF:FF:FF:FF:FF}):
          ``¿Quién tiene \texttt{192.168.1.5}? Dime tu MAC''
    \item PC-B (que tiene esa IP) responde con \textbf{ARP Reply} en unicast:
          ``Yo soy \texttt{192.168.1.5}, mi MAC es \texttt{AA:BB:CC:11:22:33}''
    \item PC-A guarda esta info en su \textbf{ARP table} (cache)
\end{enumerate}

\begin{cuidado}
\textbf{ARP Spoofing / Poisoning:} Un atacante puede responder falsamente a
un ARP Request, haciendo que el tráfico pase por su máquina (ataque MITM).
Defensa: \textbf{Dynamic ARP Inspection (DAI)} en switches modernos.
\end{cuidado}

\section{\emoji{frame-with-picture} Trama Ethernet (Ethernet Frame)}

\begin{verbatim}
Ethernet II Frame:
┌──────────┬─────────┬──────┬─────────────┬─────┐
│ Dst MAC  │ Src MAC │ Type │   Payload   │ FCS │
│  6 bytes │ 6 bytes │2 bytes│ 46-1500 B  │4 B  │
└──────────┴─────────┴──────┴─────────────┴─────┘

Type field:
  0x0800 = IPv4
  0x0806 = ARP
  0x86DD = IPv6
  0x8100 = VLAN (802.1Q)
\end{verbatim}

El \textbf{FCS} (Frame Check Sequence) es un CRC-32 para detección de errores.
Si los datos llegan corruptos, el FCS no coincide y la trama se descarta.

\section{\emoji{satellite} Hub vs Switch vs Bridge}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
 & \textbf{Hub} & \textbf{Switch} & \textbf{Bridge} \\
\midrule
Capa OSI   & 1 (Física)   & 2 (Enlace)    & 2 (Enlace) \\
Inteligencia & Ninguna   & MAC table     & MAC table \\
Reenvío    & Todos los puertos & Solo al destino & Solo al destino \\
Colisiones & Dominio único & Por puerto    & Por segmento \\
Hoy        & \emoji{skull} Obsoleto & \emoji{check-mark-button} Estándar & Reemplazado por switch \\
\bottomrule
\end{tabular}
\end{table}

\begin{ejemplo}
\textbf{¿Cómo aprende un switch?}
\begin{enumerate}
    \item PC-A (MAC \texttt{AA:AA}) envía trama por puerto 1
    \item Switch registra: ``MAC \texttt{AA:AA} está en puerto 1''
    \item Si el destino es desconocido, hace \textbf{flooding} (manda a todos)
    \item Cuando el destino responde, aprende su puerto también
    \item A partir de ahí: forwarding directo, sin flooding
\end{enumerate}
\end{ejemplo}

\section{\emoji{card-index-dividers} VLANs — Virtual LANs}

\begin{concepto}
Una \textbf{VLAN} divide lógicamente un switch físico en múltiples switches
virtuales independientes. Tráfico de VLAN 10 no puede hablar con VLAN 20
sin pasar por un router (capa 3).

\emoji{light-bulb} \textbf{Analogía:} Un edificio con varios departamentos
en el mismo edificio físico, pero con puertas separadas y sin acceso entre ellos.
\end{concepto}

La norma \textbf{IEEE 802.1Q} agrega un \textbf{tag de 4 bytes} a la trama Ethernet:
\begin{verbatim}
  802.1Q Tag:
  ┌──────┬───┬──────────────┐
  │0x8100│PCP│   VLAN ID    │
  │2 bytes│3b│   12 bits    │
  └──────┴───┴──────────────┘
  VLAN ID: 1-4094 (0 y 4095 reservados)
\end{verbatim}

\section{\emoji{arrows-counterclockwise} STP — Spanning Tree Protocol}

\begin{concepto}
\textbf{STP} (IEEE 802.1D) previene \textbf{loops} en redes con múltiples
switches. Los loops de Layer 2 son catastróficos: causan \textbf{broadcast storms}
que saturan toda la red.

\emoji{light-bulb} \textbf{Analogía:} Imagina un rumor en la escuela que se
repite infinitamente entre grupos de amigos. STP ``corta'' las conexiones
redundantes para que el rumor no circule para siempre.
\end{concepto}

RSTP (802.1w) es la versión moderna: converge en $<$1 segundo vs 30-50 segundos de STP.

\section{\emoji{chains} EtherChannel / LACP}

\begin{concepto}
\textbf{EtherChannel} agrupa múltiples enlaces físicos en uno lógico,
multiplicando el ancho de banda y agregando redundancia.

\textbf{LACP} (IEEE 802.3ad) es el protocolo estándar para negociar EtherChannel.
\end{concepto}

\begin{ejemplo}
4 cables de 1 Gbps entre dos switches \textrightarrow{} 1 enlace lógico de 4 Gbps.
Si un cable falla, el canal sigue funcionando con 3 Gbps.
\end{ejemplo}
```

- [ ] **Step 2: Compilar**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/02_capa2_enlace.tex
git commit -m "docs: cap 2 - enlace, MAC, ARP, Ethernet, VLANs, STP, EtherChannel"
git push
```

---

## Task 4: `03_capa3_red.tex` — Capa de Red

**Files:**
- Modify: `chapters/03_capa3_red.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{world-map} Capa 3 — Red (Network Layer)}

\section{\emoji{thinking-face} ¿Qué hace la capa de red?}

\begin{concepto}
La capa de red se encarga de \textbf{enrutar paquetes} entre redes distintas,
de origen a destino, aunque pasen por múltiples routers.
Usa \textbf{direcciones IP}.

\emoji{light-bulb} \textbf{Analogía:} Las MACs son como el número de asiento
en el salón (local). Las IPs son como tu dirección postal (funciona en
cualquier parte del mundo). Un router es como el servicio de correos:
sabe cómo llevar tu carta de ciudad en ciudad.
\end{concepto}

\section{\emoji{puzzle-piece} IPv4}

\subsection{Estructura del header IPv4}

\begin{verbatim}
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Ver=4| IHL |    DSCP   |ECN|          Total Length             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|    Fragment Offset      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  TTL (8b)  |  Protocol (8b)  |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source IP Address                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination IP Address                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
\end{verbatim}

Campos clave:
\begin{itemize}
    \item \textbf{TTL} (Time to Live): cada router lo decrementa en 1.
          Si llega a 0, el paquete se descarta y se envía un ICMP ``Time Exceeded''.
          Evita loops infinitos.
    \item \textbf{Protocol}: qué viene en el payload.
          6 = TCP, 17 = UDP, 1 = ICMP, 89 = OSPF.
    \item \textbf{Flags}: DF (Don't Fragment), MF (More Fragments)
\end{itemize}

\subsection{Clases de IP y CIDR}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
\textbf{Clase} & \textbf{Rango} & \textbf{Máscara default} & \textbf{Hosts} \\
\midrule
A & 1.0.0.0 – 126.255.255.255   & /8  (255.0.0.0)     & 16,777,214 \\
B & 128.0.0.0 – 191.255.255.255 & /16 (255.255.0.0)   & 65,534 \\
C & 192.0.0.0 – 223.255.255.255 & /24 (255.255.255.0) & 254 \\
\bottomrule
\end{tabular}
\end{table}

\begin{ejemplo}
\textbf{Subnetting:} Dividir \texttt{192.168.1.0/24} en 4 subredes iguales:
\begin{itemize}
    \item Nueva máscara: /26 (255.255.255.192, bloques de 64)
    \item Subred 0: \texttt{192.168.1.0/26}   — hosts \texttt{.1} a \texttt{.62}
    \item Subred 1: \texttt{192.168.1.64/26}  — hosts \texttt{.65} a \texttt{.126}
    \item Subred 2: \texttt{192.168.1.128/26} — hosts \texttt{.129} a \texttt{.190}
    \item Subred 3: \texttt{192.168.1.192/26} — hosts \texttt{.193} a \texttt{.254}
\end{itemize}
Fórmula: $2^{n}$ subredes donde $n$ = bits prestados; $2^{h}-2$ hosts donde $h$ = bits de host.
\end{ejemplo}

\subsection{IPs privadas (RFC 1918)}

\begin{table}[h!]
\centering
\begin{tabular}{ll}
\toprule
\textbf{Rango} & \textbf{Uso} \\
\midrule
10.0.0.0/8           & Redes grandes corporativas \\
172.16.0.0/12        & Redes medianas \\
192.168.0.0/16       & Redes domésticas / pequeñas \\
127.0.0.0/8          & Loopback (127.0.0.1 = ``yo mismo'') \\
\bottomrule
\end{tabular}
\end{table}

\section{\emoji{signpost} Routing — Enrutamiento}

\subsection{Routing estático}

Configurado manualmente por el administrador:
\begin{codigo}
\begin{lstlisting}
! Cisco IOS - ruta estática
ip route 10.0.2.0 255.255.255.0 192.168.1.1
! Destino        Máscara          Next-hop

! Ruta default (gateway de último recurso)
ip route 0.0.0.0 0.0.0.0 203.0.113.1
\end{lstlisting}
\end{codigo}

\subsection{OSPF — Open Shortest Path First}

\begin{concepto}
\textbf{OSPF} (RFC 2328) es un protocolo de routing dinámico de \textbf{link-state}.
Cada router conoce la topología completa de la red y calcula el camino más
corto con el \textbf{algoritmo de Dijkstra (SPF)}.
\end{concepto}

Conceptos clave de OSPF:
\begin{itemize}
    \item \textbf{Áreas:} La red se divide en áreas. El \textbf{Área 0} (backbone) es obligatoria.
    \item \textbf{LSA} (Link State Advertisement): anuncios que intercambian los routers
    \item \textbf{DR/BDR} (Designated Router): en redes multi-acceso, un router centraliza los LSAs
    \item \textbf{Costo:} métrica basada en bandwidth. Por defecto: $\text{costo} = 10^8 / \text{bandwidth}$
\end{itemize}

\subsection{BGP — Border Gateway Protocol}

\begin{concepto}
\textbf{BGP} (RFC 4271) es el protocolo de routing de Internet. Conecta
Sistemas Autónomos (AS) — grandes redes de ISPs y corporaciones.
Es el protocolo que decide \textit{cómo viajan tus datos por todo el mundo}.

\emoji{light-bulb} \textbf{Analogía:} Si OSPF es el GPS dentro de tu ciudad,
BGP es el sistema de mapas entre países. Cada país (AS) decide sus propias
reglas de tránsito.
\end{concepto}

\begin{cuidado}
\textbf{BGP Hijacking:} Un AS malicioso puede anunciar prefijos IP que no le
pertenecen, robando tráfico. Famoso caso: \textbf{Pakistan Telecom (2008)}
dejó YouTube offline en todo el mundo accidentalmente durante 2 horas.
Defensa moderna: \textbf{RPKI} (ver capítulo de seguridad).
\end{cuidado}

\section{\emoji{recycle} NAT — Network Address Translation}

\begin{concepto}
\textbf{NAT} permite que múltiples dispositivos con IPs privadas compartan
\textbf{una sola IP pública}. Es la razón por la que todos en tu casa
``comparten'' la IP del router.

\emoji{light-bulb} \textbf{Analogía:} El router es como la recepción de una oficina.
Todas las llamadas internas salen con el número de la empresa, y la recepción
sabe a qué interno reenviar cada respuesta.
\end{concepto}

\textbf{PAT} (Port Address Translation) = NAT overload: usa números de puerto
para distinguir entre múltiples conexiones con la misma IP pública.

\section{\emoji{globe-with-meridians} IPv6}

\begin{concepto}
\textbf{IPv6} (RFC 8200) tiene direcciones de 128 bits — suficientes para dar
$3.4 \times 10^{38}$ direcciones. IPv4 solo tiene $\approx 4.3$ mil millones y
ya se agotaron.
\end{concepto}

Formato: \texttt{2001:0db8:85a3:0000:0000:8a2e:0370:7334}

Tipos de direcciones IPv6:
\begin{itemize}
    \item \textbf{Link-local} (\texttt{fe80::/10}): solo en la red local, asignada automáticamente
    \item \textbf{Global unicast} (\texttt{2000::/3}): equivalente a IP pública de IPv4
    \item \textbf{Loopback:} \texttt{::1}
    \item \textbf{Multicast} (\texttt{ff00::/8}): un paquete a múltiples destinos
\end{itemize}

\begin{cuidado}
IPv6 \textbf{no tiene broadcast}. Usa multicast para funciones que en IPv4
usaban broadcast (como NDP, el equivalente a ARP).
\end{cuidado}
```

- [ ] **Step 2: Compilar y verificar**

```bash
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/03_capa3_red.tex
git commit -m "docs: cap 3 - capa red, IPv4, subnetting, OSPF, BGP, NAT, IPv6"
git push
```

---

## Task 5: `04_capa4_transporte.tex` — Capa de Transporte

**Files:**
- Modify: `chapters/04_capa4_transporte.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{truck} Capa 4 — Transporte (Transport Layer)}

\section{\emoji{thinking-face} ¿Qué hace la capa de transporte?}

\begin{concepto}
La capa de transporte entrega datos de \textbf{aplicación a aplicación}
(proceso a proceso), usando \textbf{números de puerto} para identificar qué app
recibe qué dato. Vive en los hosts extremos, \textit{no} en los routers.

\emoji{light-bulb} \textbf{Analogía:} IP sabe llegar a la \textit{casa} correcta
(host). El \textit{puerto} es el número de departamento dentro de esa casa.
El cartero (IP) deja el paquete en la puerta; el portero (transporte) sube
al departamento correcto.
\end{concepto}

\subsection{Números de puerto}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Rango} & \textbf{Tipo} & \textbf{Ejemplos} \\
\midrule
0–1023     & Well-known (reservados) & 80=HTTP, 443=HTTPS, 22=SSH, 53=DNS \\
1024–49151 & Registered               & 3306=MySQL, 5432=PostgreSQL \\
49152–65535 & Ephemeral (cliente)     & Asignados temporalmente por el OS \\
\bottomrule
\end{tabular}
\end{table}

\section{\emoji{zap} UDP — User Datagram Protocol (RFC 768)}

\begin{concepto}
\textbf{UDP} es \textbf{connectionless}: manda datagramas sin establecer conexión
previa, sin confirmar llegada, sin control de orden.

\emoji{light-bulb} \textbf{Analogía:} UDP es como mandar postales.
Las mandas y asumes que llegan. Si se pierde una... ni modo.
\end{concepto}

Header UDP (solo 8 bytes):
\begin{verbatim}
 0              15 16             31
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|   Source Port   | Dest. Port  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Length      |  Checksum   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
\end{verbatim}

Casos de uso de UDP: DNS, DHCP, streaming de video, gaming online, VoIP.
\textbf{Velocidad > confiabilidad.}

\section{\emoji{handshake} TCP — Transmission Control Protocol (RFC 793)}

\begin{concepto}
\textbf{TCP} es \textbf{connection-oriented}: establece una conexión, garantiza
entrega en orden, retransmite paquetes perdidos y controla el flujo.

\emoji{light-bulb} \textbf{Analogía:} TCP es como una llamada telefónica:
primero dices ``¿Aló?'', esperas ``Sí, te escucho'', y después de confirmar
que la conexión funciona empiezas a hablar.
\end{concepto}

\subsection{Header TCP (20 bytes mínimo)}

\begin{verbatim}
 0               15 16              31
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Source Port   |  Dest. Port   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Sequence Number          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Acknowledgment Number      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Offset|Rsv|U|A|P|R|S|F|  Window    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|    Checksum       |  Urgent Ptr   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
\end{verbatim}

\subsection{Flags TCP}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Flag} & \textbf{Nombre} & \textbf{Uso} \\
\midrule
SYN & Synchronize & Iniciar conexión \\
ACK & Acknowledge & Confirmar recepción \\
FIN & Finish      & Cerrar conexión normalmente \\
RST & Reset       & Cierre abrupto / error \\
PSH & Push        & Enviar datos inmediatamente al app \\
URG & Urgent      & Datos urgentes (raro en uso moderno) \\
\bottomrule
\end{tabular}
\end{table}

\subsection{TCP 3-Way Handshake}

\begin{center}
\begin{tikzpicture}[
    node distance=4cm,
    msg/.style={->, thick, >=stealth}
]
\node (client) at (0,0) {\textbf{Cliente}};
\node (server) at (6,0) {\textbf{Servidor}};

\draw[thick] (0,-0.3) -- (0,-5);
\draw[thick] (6,-0.3) -- (6,-5);

% SYN
\draw[msg] (0,-1) -- (6,-1.8)
    node[midway, above, sloped, font=\small] {SYN, seq=100};
% SYN-ACK
\draw[msg] (6,-1.8) -- (0,-2.8)
    node[midway, above, sloped, font=\small] {SYN-ACK, seq=300, ack=101};
% ACK
\draw[msg] (0,-2.8) -- (6,-3.6)
    node[midway, above, sloped, font=\small] {ACK, ack=301};

\node[right, font=\small\itshape] at (6,-4.2) {Conexión establecida \emoji{check-mark-button}};
\end{tikzpicture}
\end{center}

\subsection{TCP 4-Way Termination}

\begin{verbatim}
Cliente              Servidor
   |--- FIN -->          |   "Terminé de enviar"
   |<-- ACK ---          |   "Ok, recibido"
   |<-- FIN ---          |   "Yo también terminé"
   |--- ACK -->          |   "Ok, cerramos"
         (TIME_WAIT: espera 2×MSL antes de cerrar del todo)
\end{verbatim}

\subsection{Control de congestión TCP}

\begin{concepto}
TCP ajusta automáticamente su velocidad de envío para no saturar la red.
El campo \textbf{Congestion Window (cwnd)} controla cuántos bytes puede enviar
sin esperar ACK.
\end{concepto}

Fases:
\begin{enumerate}
    \item \textbf{Slow Start:} cwnd empieza en 1 MSS, se \textit{dobla} con cada ACK (crecimiento exponencial)
    \item \textbf{Congestion Avoidance:} al superar el umbral (ssthresh), crece linealmente
    \item \textbf{Fast Retransmit:} si llegan 3 ACKs duplicados, retransmite sin esperar timeout
    \item \textbf{Fast Recovery:} reduce cwnd a la mitad (no a 1) tras pérdida por 3-ACK dup
\end{enumerate}

\begin{cuidado}
\textbf{¿Por qué TCP es lento para HTTP?} Cada nueva conexión empieza slow start
desde cero. Con HTTP/1.1, abrir muchos recursos = muchas conexiones TCP = latencia acumulada.
Esto es exactamente el problema que Google resolvió con QUIC (ver capítulo 8).
\end{cuidado}
```

- [ ] **Step 2: Compilar**

```bash
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/04_capa4_transporte.tex
git commit -m "docs: cap 4 - transporte, UDP, TCP, handshake, flags, congestion control"
git push
```

---

## Task 6: `05_capa5_sesion.tex` + `06_capa6_presentacion.tex`

**Files:**
- Modify: `chapters/05_capa5_sesion.tex`
- Modify: `chapters/06_capa6_presentacion.tex`

- [ ] **Step 1: Escribir `05_capa5_sesion.tex`**

```latex
\chapter{\emoji{handshake} Capa 5 — Sesión (Session Layer)}

\begin{concepto}
La capa de sesión establece, gestiona y termina \textbf{sesiones de comunicación}
entre aplicaciones. En la práctica, sus funciones están implementadas en
protocolos de la capa de aplicación.

\emoji{warning} \textbf{Nota:} SSH técnicamente opera en la \textbf{capa 7}
(Aplicación), pero el manual MADO-31 lo clasifica en capa 5 porque gestiona
sesiones. Esta discrepancia es normal — en la práctica, los protocolos
no se alinean perfectamente con OSI.
\end{concepto}

\section{\emoji{locked-with-key} SSH — Secure Shell (RFC 4251-4254)}

\begin{concepto}
\textbf{SSH} reemplaza a Telnet para administración remota de sistemas.
Todo el tráfico está \textbf{cifrado}, incluyendo la autenticación.

\emoji{light-bulb} \textbf{Analogía:} Telnet es como hablar en voz alta en un
cuarto lleno de gente — cualquiera te escucha. SSH es como hablar en un
cuarto a prueba de sonido con candado.
\end{concepto}

\subsection{Comparativa SSH vs Telnet}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
 & \textbf{Telnet} & \textbf{SSH} \\
\midrule
Puerto   & 23         & 22 \\
Cifrado  & \emoji{cross-mark} Ninguno & \emoji{check-mark-button} AES, ChaCha20 \\
Auth     & Contraseña en texto plano & Clave pública o contraseña cifrada \\
Seguridad & \emoji{skull} Inseguro  & \emoji{shield} Seguro \\
Estado   & Obsoleto, no usar & Estándar actual \\
\bottomrule
\end{tabular}
\end{table}

\subsection{SSH Key Exchange — ¿Cómo funciona?}

\begin{verbatim}
Cliente                        Servidor
   |--- TCP SYN / connection -->    |
   |<-- SSH version string  ---     |
   |--- SSH version string  -->     |
   |<-- Server public key / ---     |
   |    DH parameters               |
   |--- DH public value     -->     |
   |    (calcula shared secret)     |
   |<-- Encrypted: OK, ready --     |
   |--- Encrypted: auth creds -->   |
   |<-- Encrypted: session   --     |
\end{verbatim}

El intercambio usa \textbf{Diffie-Hellman}: cliente y servidor derivan el mismo
\textit{shared secret} sin enviarlo nunca por la red.

\subsection{Autenticación por clave pública}

\begin{enumerate}
    \item Generas un par de claves: \texttt{ssh-keygen -t ed25519}
    \item Tu \textbf{clave pública} (\texttt{\textasciitilde/.ssh/id\_ed25519.pub}) va al servidor (\texttt{\textasciitilde/.ssh/authorized\_keys})
    \item Al conectar, el servidor cifra un reto con tu clave pública
    \item Solo quien tiene la \textbf{clave privada} puede descifrar el reto
    \item Sin contraseña por la red — más seguro y cómodo
\end{enumerate}
```

- [ ] **Step 2: Escribir `06_capa6_presentacion.tex`**

```latex
\chapter{\emoji{artist-palette} Capa 6 — Presentación (Presentation Layer)}

\begin{concepto}
La capa de presentación se encarga de:
\begin{itemize}
    \item \textbf{Codificación:} convertir datos a un formato entendible por el receptor
    \item \textbf{Compresión:} reducir el tamaño de los datos
    \item \textbf{Cifrado/Descifrado:} proteger los datos en tránsito
\end{itemize}
\end{concepto}

\section{\emoji{abc} Codificación de Caracteres}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Codificación} & \textbf{Bits} & \textbf{Cobertura} \\
\midrule
ASCII    & 7 bits  & Solo inglés (128 chars) \\
Latin-1  & 8 bits  & Europa occidental \\
UTF-8    & Variable (1-4 bytes) & Todo Unicode, compatible ASCII \\
UTF-16   & 2-4 bytes & Todo Unicode, común en Windows \\
\bottomrule
\end{tabular}
\end{table}

\begin{ejemplo}
La letra ``ñ'' en UTF-8 se representa como \texttt{0xC3 0xB1} (2 bytes).
En ASCII no existe — por eso los sistemas viejos mostraban ``Ã±''.
\end{ejemplo}

\section{\emoji{file-folder} Serialización de Datos}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
\textbf{Formato} & \textbf{Legible} & \textbf{Tamaño} & \textbf{Uso} \\
\midrule
JSON     & \emoji{check-mark-button} Sí  & Mediano & APIs REST, configs \\
XML      & \emoji{check-mark-button} Sí  & Grande  & Legacy, SOAP \\
Protobuf & \emoji{cross-mark} No (binario) & Pequeño & gRPC, microservicios \\
MessagePack & \emoji{cross-mark} No    & Muy pequeño & IoT, gaming \\
\bottomrule
\end{tabular}
\end{table}

\begin{moderno}
\textbf{Protocol Buffers (Protobuf)} — creado por Google (2008):
El mismo dato en JSON puede ocupar 200 bytes; en Protobuf, 30 bytes.
3-10x más compacto y 5-10x más rápido de serializar. Usado en gRPC.
\end{moderno}

\section{\emoji{locked} TLS — Transport Layer Security}

\begin{concepto}
\textbf{TLS} (sucesor de SSL) cifra la comunicación entre cliente y servidor.
HTTPS = HTTP + TLS. Es lo que hace que el candado aparezca en tu navegador.

\emoji{light-bulb} \textbf{Analogía:} TLS es como un sobre sellado y firmado.
El sobre garantiza que nadie lo abrió (integridad) y que viene del remitente
correcto (autenticación). El contenido es ilegible para cualquier
intermediario (confidencialidad).
\end{concepto}

\subsection{TLS 1.2 vs TLS 1.3}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
 & \textbf{TLS 1.2} & \textbf{TLS 1.3 (RFC 8446, 2018)} \\
\midrule
Handshake RTTs & 2 RTT & \textbf{1 RTT} (más rápido) \\
0-RTT resumption & No & \emoji{check-mark-button} Sí \\
Cipher suites  & 37 opciones (algunas débiles) & Solo 5 (todas seguras) \\
RSA key exchange & Permitido & \emoji{cross-mark} Eliminado \\
Perfect Forward Secrecy & Opcional & \textbf{Obligatorio} \\
\bottomrule
\end{tabular}
\end{table}

\subsection{Handshake TLS 1.3}

\begin{verbatim}
Cliente                        Servidor
   |--- ClientHello          -->    | (key_share, supported versions)
   |<-- ServerHello          ---    | (key_share seleccionado)
   |<-- {EncryptedExtensions} -     |
   |<-- {Certificate}        ---    |
   |<-- {CertificateVerify}  ---    |
   |<-- {Finished}           ---    |
   |--- {Finished}           -->    |
   |=== Application Data    ====    | ← ¡Todo cifrado desde aquí!
\end{verbatim}

TLS 1.3 usa \textbf{ECDHE} (Elliptic Curve Diffie-Hellman Ephemeral) para
Perfect Forward Secrecy: si la clave privada del servidor se compromete en el
futuro, el tráfico pasado \textit{no} se puede descifrar.
```

- [ ] **Step 3: Compilar**

```bash
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 4: Commit + push (ambos capítulos juntos)**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/05_capa5_sesion.tex chapters/06_capa6_presentacion.tex
git commit -m "docs: cap 5 y 6 - SSH, TLS 1.3, codificación, Protobuf"
git push
```

---

## Task 7: `07_capa7_aplicacion.tex` — Capa de Aplicación

**Files:**
- Modify: `chapters/07_capa7_aplicacion.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{desktop-computer} Capa 7 — Aplicación (Application Layer)}

\section{\emoji{thinking-face} ¿Qué hace la capa de aplicación?}

\begin{concepto}
La capa de aplicación es la interfaz entre los programas del usuario y la red.
Aquí viven los protocolos que usas a diario: HTTP (web), DNS (nombres de dominio),
DHCP (IPs automáticas), SMTP (correo).
\end{concepto}

\section{\emoji{satellite-antenna} DHCP — Dynamic Host Configuration Protocol}

\begin{concepto}
\textbf{DHCP} asigna automáticamente: dirección IP, máscara, gateway y DNS
a los dispositivos cuando se conectan a la red.

\emoji{light-bulb} \textbf{Analogía:} Llegar a un hotel (red) y que la recepción
(servidor DHCP) te asigne automáticamente: número de habitación (IP),
llave maestra del piso (gateway) y el directorio del hotel (DNS).
\end{concepto}

\subsection{Proceso DORA}

\begin{center}
\begin{tikzpicture}[msg/.style={->, thick, >=stealth}]
\node (client) at (0,0) {\textbf{Cliente}};
\node (server) at (7,0) {\textbf{Servidor DHCP}};
\draw[thick] (0,-0.3) -- (0,-5.5);
\draw[thick] (7,-0.3) -- (7,-5.5);

\draw[msg] (0,-1) -- (7,-1.6)
    node[midway,above,sloped,font=\small] {DISCOVER (broadcast: ``¿Hay servidor?'')};
\draw[msg] (7,-1.6) -- (0,-2.4)
    node[midway,above,sloped,font=\small] {OFFER (``Te ofrezco 192.168.1.10'')};
\draw[msg] (0,-2.4) -- (7,-3.0)
    node[midway,above,sloped,font=\small] {REQUEST (broadcast: ``Acepto 192.168.1.10'')};
\draw[msg] (7,-3.0) -- (0,-3.8)
    node[midway,above,sloped,font=\small] {ACK (``Confirmado, es tuya por 24h'')};
\end{tikzpicture}
\end{center}

\section{\emoji{globe-with-meridians} DNS — Domain Name System}

\begin{concepto}
\textbf{DNS} traduce nombres de dominio (\texttt{google.com}) a direcciones IP
(\texttt{142.250.80.46}).

\emoji{light-bulb} \textbf{Analogía:} DNS es la agenda de contactos de Internet.
No necesitas memorizar ``142.250.80.46''; solo escribes ``google.com'' y
DNS busca el número por ti.
\end{concepto}

\subsection{Jerarquía DNS}

\begin{verbatim}
         . (root)
         |
    .com  .org  .mx  .net  ...  (TLD)
         |
      google.com  (Second-level domain)
         |
  www  mail  api  (Subdomain)
\end{verbatim}

\subsection{Tipos de registros DNS}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Tipo} & \textbf{¿Qué guarda?} & \textbf{Ejemplo} \\
\midrule
A     & IPv4 del dominio         & \texttt{google.com → 142.250.80.46} \\
AAAA  & IPv6 del dominio         & \texttt{google.com → 2607:f8b0::...} \\
CNAME & Alias a otro dominio     & \texttt{www → google.com} \\
MX    & Servidor de correo       & \texttt{google.com → aspmx.l.google.com} \\
TXT   & Texto libre (SPF, DKIM)  & \texttt{"v=spf1 include:..."} \\
NS    & Nameservers del dominio  & \texttt{ns1.google.com} \\
PTR   & Reverse DNS (IP → nombre)& \texttt{46.80.250.142.in-addr.arpa → google.com} \\
\bottomrule
\end{tabular}
\end{table}

\section{\emoji{globe-showing-europe-africa} HTTP — HyperText Transfer Protocol}

\subsection{HTTP/1.1 — El original}

\begin{verbatim}
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html>...</html>
\end{verbatim}

\textbf{Problema:} Head-of-line blocking. Con una conexión TCP, si el primer
recurso tarda, todos los demás esperan en fila.

\subsection{HTTP/2 (RFC 7540, 2015)}

Mejoras clave:
\begin{itemize}
    \item \textbf{Multiplexing:} múltiples requests en \textit{una sola} conexión TCP, en paralelo
    \item \textbf{Header compression (HPACK):} los headers repetidos se comprimen
    \item \textbf{Binary framing:} texto → binario, más eficiente
    \item \textbf{Server push:} el servidor puede enviar recursos antes de que el cliente los pida
\end{itemize}

\subsection{Códigos de estado HTTP}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Código} & \textbf{Categoría} & \textbf{Ejemplos comunes} \\
\midrule
1xx & Informational & 100 Continue \\
2xx & Success       & 200 OK, 201 Created, 204 No Content \\
3xx & Redirection   & 301 Moved Permanently, 304 Not Modified \\
4xx & Client Error  & 400 Bad Request, 401 Unauthorized, 404 Not Found \\
5xx & Server Error  & 500 Internal Server Error, 503 Service Unavailable \\
\bottomrule
\end{tabular}
\end{table}
```

- [ ] **Step 2: Compilar**

```bash
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/07_capa7_aplicacion.tex
git commit -m "docs: cap 7 - aplicación, DHCP DORA, DNS, HTTP/1.1 y HTTP/2"
git push
```

---

## Task 8: `08_modernos_google.tex` — Protocolos Modernos

**Files:**
- Modify: `chapters/08_modernos_google.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{rocket} Protocolos Modernos — La Revolución de Google}

\begin{concepto}
Entre 2009 y 2024, Google diseñó o lideró la adopción de varios protocolos
que hoy mueven el 25–40\% de todo el tráfico de Internet:
SPDY \textrightarrow{} HTTP/2 \textrightarrow{} QUIC \textrightarrow{} HTTP/3.

\emoji{light-bulb} Este capítulo explica \textit{por qué} existían los problemas
y cómo cada protocolo los resolvió.
\end{concepto}

\section{\emoji{hourglass-done} El Problema: TCP + TLS es Lento}

\begin{verbatim}
Para abrir una conexión HTTPS en HTTP/1.1:

Tiempo →  [TCP SYN] [TCP SYN-ACK] [TCP ACK] = 1 RTT (TCP handshake)
          [TLS ClientHello] ... [TLS Finished] = 2 RTT (TLS 1.2 handshake)
          [HTTP GET] [HTTP 200 OK]             = 1 RTT (primera respuesta)
                                                ────────
                                                4 RTT antes de ver datos!

En QUIC + HTTP/3:
          [QUIC Initial + TLS] [QUIC Handshake Done] = 1 RTT total
          [HTTP/3 GET]                                = siguiente RTT
          O con 0-RTT: ¡datos en el primer paquete!
\end{verbatim}

\section{\emoji{wrench} SPDY — El Experimento de Google (2009–2015)}

\begin{concepto}
\textbf{SPDY} (no es acrónimo, se pronuncia ``speedy'') fue el prototipo interno
de Google para reemplazar HTTP/1.1. Introdujo multiplexing y compresión de
headers. Se volvió la base de \textbf{HTTP/2} (2015) y luego fue discontinuado.
\end{concepto}

\section{\emoji{high-voltage} QUIC — Quick UDP Internet Connections (RFC 9000, 2021)}

\begin{concepto}
\textbf{QUIC} es un protocolo de transporte que corre sobre \textbf{UDP},
integrando TLS 1.3 de forma nativa. Fue creado por Google en 2012,
estandarizado por IETF en 2021 (RFC 9000).

Hoy, \textbf{25\% del tráfico de Internet} usa QUIC (YouTube, Gmail, Google Search).
\end{concepto}

\subsection{¿Por qué UDP y no TCP?}

TCP está implementado en el \textbf{kernel del OS}. Modificarlo requiere
actualizar millones de sistemas. QUIC al correr en UDP puede evolucionar
en el \textit{espacio de usuario} — Google lo actualiza con el navegador.

\subsection{Características clave de QUIC}

\begin{enumerate}
    \item \textbf{0-RTT Connection Resumption:} si ya hablaste con el servidor antes,
          puedes enviar datos en el primer paquete. Sin handshake extra.

    \item \textbf{Streams independientes:} como HTTP/2, múltiples streams en paralelo.
          PERO: si se pierde un paquete de stream 1, los streams 2, 3, 4
          \textit{no se bloquean}. En TCP, todos esperarían.

    \item \textbf{Connection Migration:} si cambias de Wi-Fi a 4G, la conexión QUIC
          \textit{sobrevive} usando un Connection ID, no la IP. TCP se rompe.

    \item \textbf{TLS 1.3 integrado:} no es opcional como en TCP+TLS.
          No existe QUIC sin cifrado.
\end{enumerate}

\begin{verbatim}
TCP + TLS                        QUIC
┌──────────────────────┐        ┌────────────────────────────┐
│ TCP (kernel)         │        │ UDP (kernel, simple)       │
│ TLS (user space)     │        │ QUIC = Transport + TLS 1.3 │
│ HTTP/2 (user space)  │        │      (user space)          │
└──────────────────────┘        │ HTTP/3 (user space)        │
 3 capas, cada una por separado └────────────────────────────┘
                                 1 stack integrado
\end{verbatim}

\section{\emoji{globe-showing-americas} HTTP/3 (RFC 9114, 2022)}

\begin{concepto}
\textbf{HTTP/3} es HTTP sobre QUIC. Misma semántica que HTTP/2 (métodos,
headers, status codes), pero el transporte es QUIC en vez de TCP.
\end{concepto}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
 & \textbf{HTTP/1.1} & \textbf{HTTP/2} & \textbf{HTTP/3} \\
\midrule
Transporte    & TCP          & TCP          & \textbf{QUIC (UDP)} \\
Multiplexing  & \emoji{cross-mark} No & \emoji{check-mark-button} Sí & \emoji{check-mark-button} Sí \\
HOL Blocking  & \emoji{skull} Capa app + TCP & \emoji{skull} Solo TCP & \emoji{check-mark-button} Ninguno \\
0-RTT         & \emoji{cross-mark} No & \emoji{cross-mark} No & \emoji{check-mark-button} Sí \\
TLS           & Opcional     & Opcional     & \textbf{Siempre} \\
\bottomrule
\end{tabular}
\caption{Evolución de HTTP}
\end{table}

\section{\emoji{satellite} gRPC — Google Remote Procedure Call (2016)}

\begin{concepto}
\textbf{gRPC} permite llamar funciones en otro servidor como si fueran locales,
usando \textbf{HTTP/2} y \textbf{Protobuf}. Estándar en microservicios.

\emoji{light-bulb} \textbf{Analogía:} REST API es como enviar un correo pidiendo
algo. gRPC es como llamar por teléfono y hablar directamente — más rápido,
respuesta inmediata, y puedes hablar mientras el otro también habla.
\end{concepto}

Tipos de llamadas gRPC:
\begin{itemize}
    \item \textbf{Unary:} cliente envía 1 request, recibe 1 response (como REST)
    \item \textbf{Server streaming:} cliente envía 1 request, servidor responde con stream de datos
    \item \textbf{Client streaming:} cliente envía stream, servidor responde 1 vez
    \item \textbf{Bidirectional streaming:} ambos envían y reciben streams simultáneamente
\end{itemize}

\section{\emoji{chart-increasing} BBR — Bottleneck Bandwidth and RTT (Google, 2016)}

\begin{concepto}
\textbf{BBR} es un algoritmo de control de congestión creado por Google.
A diferencia de CUBIC (el default de Linux), BBR no espera a que haya
pérdida de paquetes para reducir velocidad — \textit{modela} la red para
encontrar su capacidad real.

Resultado: \textbf{2x–25x más throughput} en conexiones con pérdida de paquetes.
YouTube y Google.com usan BBR en sus servidores.
\end{concepto}

\section{\emoji{magnifying-glass-tilted-left} DNS over HTTPS — DoH (RFC 8484, 2018)}

\begin{concepto}
DNS tradicional va en \textbf{texto plano por UDP puerto 53} — cualquiera en
la red puede ver qué dominios visitas. \textbf{DoH} envuelve las consultas DNS
en HTTP/2 sobre TLS.

Google DNS: \texttt{https://dns.google/dns-query}\\
Cloudflare: \texttt{https://cloudflare-dns.com/dns-query}
\end{concepto}

\section{\emoji{video-camera} WebRTC — Real-Time Communication}

\begin{concepto}
\textbf{WebRTC} (liderado por Google, 2011) permite comunicación P2P en tiempo
real directamente en el navegador: videollamadas, VoIP, transferencia de datos.
Sin plugins, sin Flash.
\end{concepto}

Componentes:
\begin{itemize}
    \item \textbf{ICE:} descubre cómo conectar dos peers (incluso detrás de NAT)
    \item \textbf{STUN:} descubre tu IP pública
    \item \textbf{TURN:} relay si la conexión directa falla
    \item \textbf{SRTP:} cifra el audio/video
    \item \textbf{DTLS:} cifra el canal de datos (como TLS pero sobre UDP)
\end{itemize}

\section{\emoji{key} ECH — Encrypted Client Hello (TLS Extension, 2023)}

\begin{concepto}
En TLS, el \textbf{SNI} (Server Name Indication) — que le dice al servidor
a qué dominio te quieres conectar — viaja en texto plano. Cualquier
intermediario (tu ISP, un gobierno) puede ver exactamente qué sitios visitas
aunque el contenido esté cifrado.

\textbf{ECH} cifra también el SNI. Chrome lo soporta desde 2023.
\end{concepto}
```

- [ ] **Step 2: Compilar**

```bash
lualatex --interaction=nonstopmode ApuntesRedes.tex 2>&1 | grep -c "^!"
```

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/08_modernos_google.tex
git commit -m "docs: cap 8 - QUIC, HTTP/3, gRPC, BBR, DoH, WebRTC, ECH"
git push
```

---

## Task 9: `09_seguridad_redes.tex` — Seguridad

**Files:**
- Modify: `chapters/09_seguridad_redes.tex`

- [ ] **Step 1: Escribir el capítulo**

```latex
\chapter{\emoji{shield} Seguridad en Redes}

\section{\emoji{triangular-flag-on-post} CIA Triad — Los 3 pilares de seguridad}

\begin{concepto}
Toda decisión de seguridad se basa en proteger estos 3 pilares:
\begin{itemize}
    \item \emoji{locked} \textbf{Confidencialidad:} solo quien debe, puede leer los datos (cifrado)
    \item \emoji{shield} \textbf{Integridad:} los datos no fueron modificados (hash, firma digital)
    \item \emoji{check-mark-button} \textbf{Disponibilidad:} el sistema funciona cuando se necesita (redundancia, anti-DoS)
\end{itemize}
\end{concepto}

\section{\emoji{fire} Firewall}

\begin{concepto}
Un \textbf{firewall} filtra tráfico de red según reglas definidas por el administrador.
Puede bloquear o permitir tráfico basándose en IP, puerto, protocolo o estado de conexión.
\end{concepto}

\begin{table}[h!]
\centering
\begin{tabular}{lll}
\toprule
\textbf{Tipo} & \textbf{Cómo funciona} & \textbf{Limitación} \\
\midrule
Stateless (packet filter) & Examina cada paquete individualmente & No entiende contexto de conexión \\
Stateful & Rastrea el estado de conexiones TCP/UDP & No inspecciona contenido \\
NGFW (Next-Gen) & Inspecciona contenido (DPI), IDS/IPS integrado & Más costoso \\
WAF & Específico para HTTP/HTTPS & Solo protege apps web \\
\bottomrule
\end{tabular}
\end{table}

\section{\emoji{globe-with-meridians} VPN — Virtual Private Network}

\begin{concepto}
Una \textbf{VPN} crea un \textbf{túnel cifrado} sobre una red pública (Internet).
Los datos viajan cifrados como si estuvieras en la red privada.
\end{concepto}

\begin{table}[h!]
\centering
\begin{tabular}{llll}
\toprule
\textbf{Protocolo} & \textbf{Capa} & \textbf{Seguridad} & \textbf{Velocidad} \\
\midrule
IPsec    & 3 (Red)      & Alta      & Media \\
OpenVPN  & 3 (con TLS)  & Alta      & Media (overhead) \\
\textbf{WireGuard} & 3 & \textbf{Muy alta} & \textbf{Muy rápido} \\
L2TP     & 2            & Media     & Media \\
\bottomrule
\end{tabular}
\end{table}

\subsection{WireGuard (2020)}

\begin{moderno}
\textbf{WireGuard} es el VPN moderno incluido en el kernel Linux desde 5.6.
Solo tiene \textbf{$\sim$4,000 líneas de código} vs OpenVPN con $\sim$400,000.
Menos código = menor superficie de ataque = más auditable.

Criptografía: Curve25519 (DH), ChaCha20 (cifrado), Poly1305 (MAC).
Sin negociación de algoritmos: una sola suite criptográfica, bien elegida.
\end{moderno}

\section{\emoji{spider-web} Zero Trust — BeyondCorp (Google)}

\begin{concepto}
El modelo tradicional asume: ``si estás dentro de la red corporativa, eres
de confianza''. \textbf{Zero Trust} dice: ``\textbf{nunca confíes, siempre verifica}'',
independientemente de si estás dentro o fuera.

\emoji{light-bulb} \textbf{Analogía:} En un banco tradicional, si tienes el
uniforme de empleado puedes moverte libremente. Zero Trust es como un banco
donde cada puerta, cajón y sala requiere credencial propia.
\end{concepto}

\textbf{BeyondCorp} (Google, 2014): Google eliminó la VPN corporativa.
Cada acceso se valida por: identidad del usuario, estado del dispositivo,
ubicación y riesgo — no por estar ``dentro'' de la red.

\section{\emoji{bug} Ataques Comunes en Redes}

\subsection{ARP Spoofing / Poisoning}

\begin{verbatim}
Red normal:
  PC-A (192.168.1.10) → ARP → Router (192.168.1.1)

Con atacante:
  Atacante envía ARP Reply falso:
  "192.168.1.1 está en MAC AA:BB:CC" (la MAC del atacante)
  Ahora PC-A manda todo el tráfico al atacante → MITM
\end{verbatim}

Defensa: \textbf{Dynamic ARP Inspection (DAI)} en el switch.

\subsection{DNS Spoofing}

Responder con una IP falsa a consultas DNS para redirigir usuarios a
sitios falsos. Defensa: \textbf{DNSSEC} (firmas criptográficas en respuestas DNS).

\subsection{BGP Hijacking}

Un AS anuncia prefijos IP que no le pertenecen para robar o espiar tráfico.
Famoso: Pakistan Telecom (2008) dejó YouTube offline globalmente.

Defensa: \textbf{RPKI} (Resource Public Key Infrastructure) —
los dueños de prefijos firman criptográficamente sus anuncios BGP.
Los routers verifican la firma antes de aceptar la ruta.

\subsection{DoS / DDoS}

\begin{itemize}
    \item \textbf{DoS:} un solo host satura un servicio con tráfico basura
    \item \textbf{DDoS:} miles de hosts (botnet) coordinan el ataque
    \item \textbf{Amplification:} usa UDP para amplificar tráfico (DNS amplification: 1 byte enviado → 100 bytes al objetivo)
\end{itemize}

Defensa: rate limiting, anycast, CDN, scrubbing centers (Cloudflare, Akamai).

\section{\emoji{locked-with-key} mTLS — Mutual TLS}

\begin{concepto}
En TLS normal, solo el cliente verifica la identidad del servidor (HTTPS).
En \textbf{mTLS}, \textit{ambos} se verifican mutuamente.

Uso: microservicios en Kubernetes (service mesh: Istio, Linkerd),
APIs machine-to-machine donde ambos lados deben autenticarse.
\end{concepto}
```

- [ ] **Step 2: Compilar completo**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes.tex
lualatex --interaction=nonstopmode ApuntesRedes.tex  # segunda pasada para ToC
grep -c "^!" ApuntesRedes.log
```
Esperado: `0` errores. El PDF final debe tener índice completo.

- [ ] **Step 3: Commit + push**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git add chapters/09_seguridad_redes.tex
git commit -m "docs: cap 9 - seguridad, VPN, WireGuard, Zero Trust BeyondCorp, ataques, RPKI"
git push
```

---

## Self-Review

**Spec coverage:**
- [x] Spanglish técnico — en todas las explicaciones
- [x] Emojis abundantes — en capítulos, secciones y cajas
- [x] Analogías simples — al inicio de cada sección `\emoji{light-bulb} Analogía:`
- [x] Profundidad técnica — headers de paquetes, algoritmos, comparativas
- [x] Diagramas TikZ — TCP handshake (cap 4), OSI model (cap 0), DHCP DORA (cap 7)
- [x] Contenido del manual MADO-31 cubierto — UTP (cap 1), switch/hub (cap 2), routing (cap 3), TCP/UDP (cap 4), SSH (cap 5), DHCP (cap 7), VPN/Firewall (cap 9)
- [x] Protocolos modernos Google — QUIC, HTTP/3, gRPC, BBR, DoH, WebRTC, ECH (cap 8)
- [x] Commit + push por capítulo — en cada Task, Step 3
- [x] PDF subible al repo — `.gitignore` solo excluye `ApuntesRedes.pdf` compilado, no el manual

**Placeholder scan:** Ningún TODO/TBD en el plan.

**Type consistency:** Todas las cajas (`concepto`, `ejemplo`, `cuidado`, `moderno`, `codigo`) definidas en `ApuntesRedes.tex` Task 0 y usadas consistentemente en todos los capítulos.
