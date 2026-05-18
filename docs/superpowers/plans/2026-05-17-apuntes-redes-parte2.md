# Apuntes Redes de Datos — Parte 2 (Nivel Senior) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create ApuntesRedes_Parte2.tex with 9 senior-level networking chapters in the same LaTeX style as Part 1, inside the same repo.

**Architecture:** Rename existing root to ApuntesRedes_Parte1.tex, create new ApuntesRedes_Parte2.tex root pointing to chapters_parte2/, same preamble/environments/compilation pipeline.

**Tech Stack:** LuaLaTeX, emoji (Segoe UI Emoji), tcolorbox, TikZ, listings, babel{spanish}, booktabs. Windows MiKTeX 25.x.

---

## Critical Rules (read before any task)

1. **Emoji in headings:** always use `\eh{name}` macro, NEVER `\emoji{name}` directly in `\chapter`, `\section`, `\subsection`.
2. **No floats inside tcolorbox:** `\begin{table}[h!]` inside `concepto/cuidado/ejemplo/moderno/codigo` causes "Not in outer par mode". Use `\begin{center}...\end{center}` with bare `tabular` instead.
3. **Stale .aux files cause false errors:** always run `rm -f *.aux *.log *.out *.toc` before compiling.
4. **Log file name matches root:** root is `ApuntesRedes_Parte2.tex` → log is `ApuntesRedes_Parte2.log`.
5. **Known invalid emoji names:** `antenna`, `wireless`, `signpost`, `layer-cake`, `identification-card`. Use: `satellite-antenna`, `birthday-cake`, `id-button`, `right-arrow-curving-up`.
6. **Compile command:** `lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex`
7. **Success check:** `grep -c "^!" ApuntesRedes_Parte2.log` must return `0`.

---

## File Map

| Action | Path |
|--------|------|
| Rename | `ApuntesRedes.tex` → `ApuntesRedes_Parte1.tex` |
| Rename | `ApuntesRedes.pdf` → `ApuntesRedes_Parte1.pdf` |
| Create | `ApuntesRedes_Parte2.tex` |
| Create | `chapters_parte2/00_intro_p2.tex` |
| Create | `chapters_parte2/01_wireless_empresarial.tex` |
| Create | `chapters_parte2/02_switching_avanzado.tex` |
| Create | `chapters_parte2/03_sdn_openflow.tex` |
| Create | `chapters_parte2/04_datacenter_vxlan_evpn.tex` |
| Create | `chapters_parte2/05_mpls_qos.tex` |
| Create | `chapters_parte2/06_kubernetes_networking.tex` |
| Create | `chapters_parte2/07_cloud_networking.tex` |
| Create | `chapters_parte2/08_multicast.tex` |

---

## Task 0: Setup — Rename Part 1 + Scaffold Part 2

**Files:**
- Rename: `ApuntesRedes.tex` → `ApuntesRedes_Parte1.tex`
- Rename: `ApuntesRedes.pdf` → `ApuntesRedes_Parte1.pdf`
- Create: `ApuntesRedes_Parte2.tex`
- Create: `chapters_parte2/` with placeholder files

- [ ] **Step 1: Rename Part 1 files**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
git mv ApuntesRedes.tex ApuntesRedes_Parte1.tex
git mv ApuntesRedes.pdf ApuntesRedes_Parte1.pdf
```

- [ ] **Step 2: Create chapters_parte2 folder with placeholders**

```bash
mkdir chapters_parte2
```

Create each of these files with content `% TODO`:
- `chapters_parte2/00_intro_p2.tex`
- `chapters_parte2/01_wireless_empresarial.tex`
- `chapters_parte2/02_switching_avanzado.tex`
- `chapters_parte2/03_sdn_openflow.tex`
- `chapters_parte2/04_datacenter_vxlan_evpn.tex`
- `chapters_parte2/05_mpls_qos.tex`
- `chapters_parte2/06_kubernetes_networking.tex`
- `chapters_parte2/07_cloud_networking.tex`
- `chapters_parte2/08_multicast.tex`

- [ ] **Step 3: Create ApuntesRedes_Parte2.tex**

```latex
% ApuntesRedes_Parte2.tex — Parte 2: Nivel Senior
\documentclass[12pt, a4paper]{book}

% Encoding & Language
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[spanish, es-tabla]{babel}

% Emojis (requiere LuaLaTeX)
\usepackage{emoji}
\setemojifont{Segoe UI Emoji}

% Iconos extra
\usepackage{fontawesome5}

% Layout
\usepackage[top=2.5cm, bottom=2.5cm, left=3cm, right=3cm]{geometry}
\usepackage{hyperref}
\hypersetup{
    colorlinks=true,
    linkcolor=blue!70!black,
    urlcolor=blue!70!black,
    pdftitle={Apuntes de Redes de Datos --- Parte 2},
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
    breaklines=true
}

% Diagramas
\usepackage{tikz}
\usetikzlibrary{shapes, arrows.meta, positioning, calc, decorations.pathreplacing}

% Matemáticas
\usepackage{amsmath}

% Colores
\usepackage{xcolor}

% Tablas
\usepackage{booktabs}
\usepackage{multirow}
\usepackage{array}

% Gráficos
\usepackage{graphicx}
\graphicspath{{assets/}}

% Macro para emojis en headings (evita MakeUppercase bug)
\newcommand{\eh}[1]{\texorpdfstring{\emoji{#1}}{}}

%% ============================================================
\begin{document}

% Evitar que \MakeUppercase del book class rompa emojis en running headers
\renewcommand{\chaptermark}[1]{\markboth{\chaptername\ \thechapter.\ #1}{}}
\renewcommand{\sectionmark}[1]{\markright{\thesection.\ #1}}

% Portada
\begin{titlepage}
    \centering
    \vspace*{2cm}
    {\Huge\bfseries \emoji{rocket} Apuntes de Redes de Datos\par}
    \vspace{0.5cm}
    {\Large\bfseries Parte 2 --- Nivel Senior\par}
    \vspace{1cm}
    {\large SDN, Datacenter, Cloud, Kubernetes, MPLS, Multicast\par}
    \vspace{0.5cm}
    {\large Aldo Zepeda Moctezuma\par}
    \vspace{0.5cm}
    {\normalsize \today\par}
    \vspace{2cm}
    {\large\itshape ``La infraestructura que no entiendes es la infraestructura que te va a fallar a las 3am.''\\[4pt]
    --- Sabiduría de SRE\par}
\end{titlepage}

\tableofcontents
\newpage

% Capítulos
\input{chapters_parte2/00_intro_p2}
\input{chapters_parte2/01_wireless_empresarial}
\input{chapters_parte2/02_switching_avanzado}
\input{chapters_parte2/03_sdn_openflow}
\input{chapters_parte2/04_datacenter_vxlan_evpn}
\input{chapters_parte2/05_mpls_qos}
\input{chapters_parte2/06_kubernetes_networking}
\input{chapters_parte2/07_cloud_networking}
\input{chapters_parte2/08_multicast}

\end{document}
```

- [ ] **Step 4: Compile to verify setup**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0` errors. PDF output written (few pages, just placeholders).

- [ ] **Step 5: Commit**

```bash
git add ApuntesRedes_Parte2.tex chapters_parte2/
git commit -m "chore: renombrar Parte 1 + scaffold Parte 2 con 9 placeholders"
git push
```

---

## Task 1: Cap 00 — Intro Parte 2

**Files:**
- Modify: `chapters_parte2/00_intro_p2.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{map} Introducción --- Parte 2: Nivel Senior}

\begin{concepto}
La Parte 1 cubrió los fundamentos: el modelo OSI, TCP/IP, los protocolos
de las 7 capas, y las tecnologías modernas de Google. Si llegaste hasta
aquí, ya sabes cómo funciona Internet.

Esta Parte 2 cubre cómo funcionan las redes \textit{por dentro}: el datacenter
de AWS, la red de un carrier como Telmex, la infraestructura de Kubernetes,
y la seguridad a nivel de switch empresarial. Son los temas que separan
a un administrador de redes junior de un Senior Network Engineer o SRE.
\end{concepto}

\section{\eh{building-construction} El Stack del Datacenter Moderno}

\begin{verbatim}
  Internet
      │
  Edge Routers (BGP con el mundo)
      │
  Firewall / DDoS scrubbing
      │
  Load Balancers (L4/L7)
      │
  Spine Switches (L3, ECMP, sin STP)
  ╔══╤══╤══╗
  ║  │  │  ║  (cada Spine conecta con TODOS los Leaf)
  ╚══╧══╧══╝
  Leaf Switches (VxLAN VTEP, acceso a servidores)
      │
  Servidores (Kubernetes Nodes / VMs)
      │
  Pods / Contenedores (CNI, eBPF)
\end{verbatim}

\section{\eh{world-map} Mapa de Tecnologías de la Parte 2}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{lll}
\toprule
\textbf{Capítulo} & \textbf{Tecnología} & \textbf{Dónde vive} \\
\midrule
01 & WPA3, 802.1X, RADIUS    & Acceso wireless empresarial \\
02 & MSTP, MACsec, QinQ      & Switches L2 avanzados \\
03 & SDN, OpenFlow            & Control plane desacoplado \\
04 & VxLAN, EVPN, Spine-Leaf  & Datacenter overlay \\
05 & MPLS, QoS, DSCP          & Backbone carrier / WAN \\
06 & CNI, kube-proxy, Istio   & Kubernetes / containers \\
07 & AWS VPC, Azure VNet      & Cloud pública \\
08 & IGMP, PIM-SM, Multicast  & Distribución 1-a-muchos \\
\bottomrule
\end{tabular}
\caption{Mapa de tecnologías Parte 2}
\end{table}

\section{\eh{bar-chart} Parte 1 vs Parte 2}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{ll}
\toprule
\textbf{Parte 1 (Fundamentos)} & \textbf{Parte 2 (Senior)} \\
\midrule
TCP/UDP, IP, DNS, HTTP          & MPLS, VxLAN, EVPN, OpenFlow \\
TLS, SSH, WireGuard             & MACsec, 802.1X, mTLS en mesh \\
Wi-Fi básico (802.11ax)         & WPA3-Enterprise, RADIUS \\
BGP básico (routing de Internet)& BGP EVPN (routing de datacenter) \\
Kubernetes mencionado           & Kubernetes networking profundo \\
AWS/Azure mencionado            & VPC, VNet, Transit Gateway \\
Multicast mencionado            & IGMP, PIM-SM, RP, SPT \\
\bottomrule
\end{tabular}
\caption{Scope Parte 1 vs Parte 2}
\end{table}

\begin{moderno}
\textbf{\emoji{rocket} Por qué importa esto hoy:} el 90\% de la infraestructura
empresarial corre en alguna combinación de Kubernetes + nube pública + datacenter
propio conectado con MPLS. Las entrevistas de SRE, Network Engineer, y DevOps
senior preguntan exactamente estos temas: VxLAN, BGP EVPN, CNI plugins,
VPC design, QoS para VoIP.
\end{moderno}
```

- [ ] **Step 2: Compile**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/00_intro_p2.tex
git commit -m "docs: parte2 cap 0 - intro, stack datacenter, mapa tecnologías"
git push
```

---

## Task 2: Cap 01 — Wireless Empresarial

**Files:**
- Modify: `chapters_parte2/01_wireless_empresarial.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{satellite-antenna} Wireless Empresarial --- WPA3 y 802.1X}

\begin{concepto}
El Wi-Fi de tu casa usa una contraseña compartida (WPA2-Personal / PSK).
Cualquiera que sepa la contraseña entra. En una empresa con 500 empleados,
eso es inaceptable: necesitas que cada empleado tenga sus propias credenciales,
que un ex-empleado no pueda conectarse al día siguiente de ser despedido,
y que el tráfico esté cifrado incluso del empleado A al empleado B.

\emoji{light-bulb} \textbf{Analogía:} Wi-Fi personal = llave maestra que
todos tienen. Wi-Fi empresarial = tarjeta de acceso individual con tu foto
y que puedes cancelar al instante.
\end{concepto}

\section{\eh{locked} WPA3 --- Wi-Fi Protected Access 3}

\subsection{WPA2 vs WPA3}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{lll}
\toprule
\textbf{Característica} & \textbf{WPA2} & \textbf{WPA3} \\
\midrule
Key Exchange     & PSK (Pre-Shared Key)     & SAE (Dragonfly) \\
Forward Secrecy  & \emoji{cross-mark} No    & \emoji{check-mark-button} Sí \\
Offline attacks  & Vulnerable (PMKID/KRACK) & Resistente \\
Open networks    & Sin cifrado              & OWE (cifrado sin contraseña) \\
Enterprise mode  & WPA2-Enterprise (802.1X) & WPA3-Enterprise (192-bit) \\
\bottomrule
\end{tabular}
\caption{WPA2 vs WPA3}
\end{table}

\subsection{SAE --- Simultaneous Authentication of Equals}

\begin{concepto}
\textbf{SAE} (también llamado Dragonfly Handshake) reemplaza PSK en WPA3.
La diferencia clave: en WPA2-PSK, la contraseña se usa directamente para
derivar la clave de sesión. Si alguien captura el handshake, puede hacer
un ataque de diccionario offline.

En SAE, cliente y AP negocian una clave sin revelar nunca la contraseña
en la red. Es \textbf{zero-knowledge proof}: demuestras que conoces la
contraseña sin enviarla.
\end{concepto}

\begin{cuidado}
\textbf{KRACK Attack (2017):} vulnerabilidad en WPA2 que permitía forzar
reinstalación de claves de cifrado, decifrar tráfico. Afectó a todos los
dispositivos WPA2. WPA3 con SAE es inmune por diseño: incluso si alguien
captura todo el handshake SAE, no puede derivar la clave de sesión sin
conocer la contraseña original.
\end{cuidado}

\subsection{OWE --- Opportunistic Wireless Encryption}

Red Wi-Fi abierta sin contraseña (aeropuerto, café) normalmente = sin cifrado.
OWE cifra el tráfico de cada cliente con un intercambio Diffie-Hellman anónimo,
sin requerir contraseña. El usuario no nota diferencia, pero el tráfico va cifrado.
Protege contra sniffing pasivo, no contra ataques activos.

\section{\eh{shield} 802.1X --- Port-Based Network Access Control}

\begin{concepto}
\textbf{802.1X} es el estándar de autenticación para acceso a redes, tanto
Wi-Fi como cableado. Define tres actores:

\begin{enumerate}
    \item \textbf{Supplicant:} el cliente (laptop, teléfono) que quiere acceso
    \item \textbf{Authenticator:} el switch o AP que controla el acceso al puerto
    \item \textbf{Authentication Server:} servidor RADIUS que verifica credenciales
\end{enumerate}

El puerto/radio permanece en estado \textbf{unauthorized} hasta que el servidor
RADIUS aprueba al cliente. Sin aprobación: sin red, sin importar la VLAN.
\end{concepto}

\subsection{EAP --- Extensible Authentication Protocol}

EAP es el protocolo que viaja dentro de 802.1X. Define cómo se autentican
el supplicant y el servidor. Hay múltiples ``métodos EAP'':

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{llll}
\toprule
\textbf{Método} & \textbf{Credencial cliente} & \textbf{Seguridad} & \textbf{Uso} \\
\midrule
EAP-TLS   & Certificado X.509      & \emoji{check-mark-button}\emoji{check-mark-button}\emoji{check-mark-button} Máxima & Enterprises con PKI \\
PEAP      & Contraseña en TLS tunnel & \emoji{check-mark-button}\emoji{check-mark-button} Alta & Active Directory \\
EAP-TTLS  & Contraseña en TLS tunnel & \emoji{check-mark-button}\emoji{check-mark-button} Alta & Linux, BYOD \\
EAP-MD5   & Contraseña hasheada    & \emoji{skull} Rota       & No usar \\
\bottomrule
\end{tabular}
\caption{Métodos EAP}
\end{table}

\subsection{RADIUS --- Remote Authentication Dial-In User Service}

\textbf{RADIUS} (RFC 2865) es el protocolo del Authentication Server.
El Authenticator (switch/AP) habla RADIUS con el servidor:

\begin{verbatim}
  Puertos: UDP 1812 (autenticación), UDP 1813 (accounting)
  Seguridad: shared secret entre AP y servidor RADIUS

  Mensajes:
  Access-Request  → "¿Puede entrar juan@empresa.com?"
  Access-Accept   ← "Sí, asígnale VLAN 20"
  Access-Reject   ← "No, credenciales inválidas"
  Access-Challenge← "Necesito más info (para PEAP/EAP-TLS)"
\end{verbatim}

RADIUS puede consultar a Active Directory, LDAP, o una base de datos
local para verificar credenciales.

\subsection{Flujo completo 802.1X con PEAP}

\begin{center}
\begin{tikzpicture}[
    node distance=1cm,
    box/.style={rectangle, draw, thick, minimum width=2.5cm, minimum height=0.7cm, align=center, font=\small\bfseries},
    msg/.style={-{Stealth}, thick},
    lbl/.style={font=\tiny, align=center}
]
\node[box] (sup) at (0,0) {Supplicant\\(Laptop)};
\node[box] (auth) at (5,0) {Authenticator\\(Switch/AP)};
\node[box] (rad) at (10,0) {RADIUS\\Server};
\node[box] (ad) at (10,-3) {Active\\Directory};

\draw[thick] (0,-0.35) -- (0,-6);
\draw[thick] (5,-0.35) -- (5,-6);
\draw[thick] (10,-0.35) -- (10,-6);

\draw[msg] (0,-1.0) -- (5,-1.0) node[midway, above, lbl] {EAPOL-Start};
\draw[msg] (5,-1.5) -- (0,-1.5) node[midway, above, lbl] {EAP-Request Identity};
\draw[msg] (0,-2.0) -- (5,-2.0) node[midway, above, lbl] {EAP-Response: juan@empresa.com};
\draw[msg] (5,-2.5) -- (10,-2.5) node[midway, above, lbl] {RADIUS Access-Request};
\draw[msg] (5,-3.0) -- (0,-3.0) node[midway, above, lbl] {EAP-Request: TLS tunnel};
\draw[msg, dashed] (10,-3.2) -- (10,-3.8) node[midway, right, lbl] {Verifica AD};
\draw[msg] (10,-4.0) -- (5,-4.0) node[midway, above, lbl] {RADIUS Access-Accept + VLAN};
\draw[msg] (5,-4.5) -- (0,-4.5) node[midway, above, lbl] {EAP-Success};
\node[font=\small\itshape, text=green!60!black] at (5,-5.5) {\emoji{check-mark-button} Puerto autorizado, VLAN 20 asignada};
\end{tikzpicture}
\end{center}

\begin{moderno}
\textbf{\emoji{rocket} EAP-TLS en Google y grandes empresas:} Google BeyondCorp
usa EAP-TLS donde el certificado del dispositivo (no del usuario) autentica
al switch. Un dispositivo no administrado --- aunque tenga las credenciales
del usuario --- no pasa el 802.1X. El certificado lo gestiona la PKI corporativa
y se revoca automáticamente cuando el dispositivo sale del inventario.
\end{moderno}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/01_wireless_empresarial.tex
git commit -m "docs: parte2 cap 1 - WPA3, SAE, 802.1X, EAP, RADIUS, flujo TikZ"
git push
```

---

## Task 3: Cap 02 — Switching Avanzado

**Files:**
- Modify: `chapters_parte2/02_switching_avanzado.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{electric-plug} Switching Avanzado}

\begin{concepto}
Los switches de Part 1 cubrían lo básico: VLANs, STP, EtherChannel.
Un switch empresarial en un datacenter o campus corporativo tiene muchas más
funciones: múltiples instancias STP por VLAN, cifrado en cada enlace físico,
transporte de VLANs de clientes sobre la red del carrier, y protección
contra tormentas de tráfico.
\end{concepto}

\section{\eh{deciduous-tree} MSTP --- Multiple Spanning Tree Protocol (802.1s)}

\begin{concepto}
\textbf{El problema con RSTP:} una sola instancia STP controla todas las VLANs.
Si tienes 100 VLANs, todas siguen el mismo árbol de spanning --- algunos links
están bloqueados para todas las VLANs aunque pudieran usarse para otras.

\emoji{light-bulb} \textbf{Analogía:} RSTP es como tener un solo semáforo
para todas las calles de una ciudad. MSTP es tener semáforos independientes
por avenida --- puedes tener flujo en la Reforma mientras Insurgentes está
en rojo.
\end{concepto}

MSTP agrupa VLANs en \textbf{instancias MST}. Cada instancia tiene su propio
árbol STP con su propio root bridge y sus propios puertos bloqueados.

\begin{verbatim}
  Sin MSTP (RSTP):
  VLAN 10, 20, 30, 40 → misma instancia STP → mismo root → mismos links bloqueados

  Con MSTP:
  MST Instance 1 → VLAN 10, 20 → Root: Switch-A → Link X activo
  MST Instance 2 → VLAN 30, 40 → Root: Switch-B → Link Y activo
  Resultado: load balancing real entre VLANs
\end{verbatim}

\begin{codigo}
\begin{lstlisting}
! Configuración MSTP (Cisco IOS):
spanning-tree mode mst

spanning-tree mst configuration
 name REGION_PRODUCCION
 revision 1
 instance 1 vlan 10, 20
 instance 2 vlan 30, 40

spanning-tree mst 1 root primary
spanning-tree mst 2 root secondary
\end{lstlisting}
\end{codigo}

\section{\eh{locked-with-key} MACsec --- IEEE 802.1AE}

\begin{concepto}
\textbf{MACsec} cifra cada frame Ethernet entre dos dispositivos adyacentes
(switch-a-switch o switch-a-servidor). Es \textbf{hop-by-hop}: cifra el enlace
físico, no el path completo.

\emoji{light-bulb} \textbf{Analogía:} TLS es como un sobre sellado que va
de tu casa al destino final. MACsec es como una caja de seguridad que se
abre y vuelve a cerrar en cada parada del camión de entrega. El contenido
siempre está cifrado en cada segmento físico.
\end{concepto}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Característica} & \textbf{TLS} & \textbf{MACsec} \\
\midrule
Capa          & L7 (aplicación)   & L2 (enlace) \\
Scope         & End-to-end        & Hop-by-hop \\
Overhead      & Headers TLS       & 32 bytes por frame \\
Transparente  & A nivel red       & A nivel aplicación \\
Uso           & HTTPS, APIs       & Links switch-switch \\
\bottomrule
\end{tabular}
\caption{TLS vs MACsec}
\end{table}

MACsec usa \textbf{MKA} (MACsec Key Agreement) para intercambiar claves entre
los dos extremos del enlace. La criptografía es AES-GCM-128 o AES-GCM-256.

\section{\eh{package} QinQ --- IEEE 802.1ad (Double Tagging)}

\begin{concepto}
\textbf{El problema:} un ISP que da servicio a múltiples clientes empresariales.
El cliente A usa VLANs 1--100. El cliente B también usa VLANs 1--100. Si el
carrier transporta ambos en su red, las VLANs se mezclan.

\textbf{QinQ} añade un segundo tag VLAN (S-Tag del carrier) afuera del tag
del cliente (C-Tag). El carrier ve solo su S-Tag; el C-Tag del cliente
viaja opaco dentro.
\end{concepto}

\begin{verbatim}
  Frame normal 802.1Q:
  [ Dst MAC | Src MAC | 0x8100 | VLAN 50 | EtherType | Datos ]
                         ^--- tag del cliente

  Frame QinQ 802.1ad:
  [ Dst MAC | Src MAC | 0x88A8 | VLAN 200 | 0x8100 | VLAN 50 | EtherType | Datos ]
                         ^--- S-Tag carrier    ^--- C-Tag cliente (opaco para el carrier)
\end{verbatim}

\section{\eh{office-building} Private VLANs (PVLAN)}

\begin{concepto}
\textbf{Escenario:} datacenter de hosting donde múltiples clientes tienen
servidores en la misma subred IP (mismo /24). Necesitas que los servidores
del cliente A no puedan comunicarse directamente con los del cliente B,
aunque estén en la misma VLAN.

Private VLANs dividen una VLAN primaria en subdominios aislados.
\end{concepto}

Tipos de puertos PVLAN:
\begin{itemize}
    \item \textbf{Promiscuous:} habla con todos los tipos (el router/gateway)
    \item \textbf{Isolated:} solo habla con Promiscuous (servidores de diferentes clientes)
    \item \textbf{Community:} habla con su comunidad + Promiscuous (servidores del mismo cliente)
\end{itemize}

\begin{verbatim}
  PVLAN 100 (primaria):
    Puerto router    → Promiscuous
    Server Cliente A → Community 101 (habla con otros de comunidad 101 + router)
    Server Cliente B → Isolated   (solo habla con el router)
    Server Cliente C → Isolated   (solo habla con el router)
\end{verbatim}

\section{\eh{ear} IGMP Snooping}

\begin{concepto}
Sin IGMP Snooping: cuando un servidor envía tráfico multicast, el switch
lo \textbf{floodea} a todos los puertos (como broadcast). Esto desperdicia
ancho de banda --- hosts que no quieren el stream lo reciben igual.

Con \textbf{IGMP Snooping}: el switch ``espía'' los mensajes IGMP entre
hosts y routers. Cuando un host envía IGMP Join para el grupo 239.1.1.1,
el switch registra ese puerto como interesado. El tráfico multicast solo
va a esos puertos.
\end{concepto}

\begin{verbatim}
  Sin IGMP Snooping:
  Servidor multicast → Switch → Puerto 1, 2, 3, 4, 5 (todos)

  Con IGMP Snooping:
  Host en puerto 2 envía IGMP Join 239.1.1.1
  Host en puerto 4 envía IGMP Join 239.1.1.1
  Switch registra: grupo 239.1.1.1 → puertos {2, 4}
  Servidor multicast → Switch → Puerto 2, 4 (solo los interesados)
\end{verbatim}

\section{\eh{warning} Storm Control}

\begin{concepto}
Una \textbf{broadcast storm} ocurre cuando un loop de red (o dispositivo
defectuoso) genera tráfico que se multiplica exponencialmente. STP previene
loops, pero si ocurren (cable mal conectado, bug), el tráfico puede saturar
todo el ancho de banda en segundos.

\textbf{Storm Control} monitorea el porcentaje de ancho de banda usado por
broadcast/multicast/unknown-unicast. Si supera el umbral, el switch descarta
el exceso o apaga el puerto.
\end{concepto}

\begin{codigo}
\begin{lstlisting}
! Storm Control en Cisco IOS (por interfaz):
interface GigabitEthernet0/1
 storm-control broadcast level 20 10
 ! nivel de corte: 20%, nivel de recuperación: 10%
 storm-control action shutdown
 ! acción: apagar el puerto si supera el umbral
\end{lstlisting}
\end{codigo}

\section{\eh{id-button} 802.1X en Switches Cableados (Wired NAC)}

\begin{concepto}
El mismo 802.1X del Wi-Fi empresarial aplica a puertos Ethernet físicos.
Un empleado que conecta su laptop a un jack de red en la oficina debe
autenticarse antes de recibir acceso a la red.
\end{concepto}

\textbf{MAB --- MAC Authentication Bypass:} dispositivos sin supplicant
(impresoras, teléfonos IP, cámaras) no pueden hacer 802.1X. MAB autentica
por dirección MAC en lugar de credenciales. El RADIUS valida la MAC contra
una lista de MACs aprobadas.

\begin{cuidado}
\textbf{MAB es débil:} las MACs se pueden suplantar. Un atacante que conozca
la MAC de una impresora puede conectar su laptop con esa MAC y pasar MAB.
Por eso MAB se combina con Dynamic ARP Inspection, DHCP Snooping y
restricciones de VLAN para limitar qué puede hacer el dispositivo autenticado.
\end{cuidado}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/02_switching_avanzado.tex
git commit -m "docs: parte2 cap 2 - MSTP, MACsec, QinQ, Private VLANs, IGMP Snooping, Storm Control"
git push
```

---

## Task 4: Cap 03 — SDN + OpenFlow

**Files:**
- Modify: `chapters_parte2/03_sdn_openflow.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{control-knobs} SDN --- Software Defined Networking}

\begin{concepto}
En el networking tradicional, cada switch y router tiene su propio cerebro
(control plane) y sus propios brazos (data plane). Para cambiar cómo se
enruta el tráfico, debes reconfigurar cada dispositivo individualmente ---
puede ser cientos de dispositivos.

\textbf{SDN} separa el cerebro (control plane) de los brazos (data plane).
Un controlador centralizado toma todas las decisiones; los switches solo
ejecutan instrucciones.

\emoji{light-bulb} \textbf{Analogía:} networking tradicional = cada taxista
decide su propia ruta. SDN = Uber, donde un algoritmo central asigna rutas
a todos los taxis simultáneamente.
\end{concepto}

\section{\eh{building-construction} Arquitectura SDN}

\begin{center}
\begin{tikzpicture}[
    layer/.style={rectangle, draw, thick, minimum width=8cm, minimum height=1.2cm,
                  align=center, font=\small\bfseries},
    arrow/.style={-{Stealth}, thick}
]
\node[layer, fill=violet!15] (app) at (0, 4) {Application Layer\\Aplicaciones de red (monitoring, load balancing, QoS)};
\node[layer, fill=blue!15] (ctrl) at (0, 2) {Control Layer\\SDN Controller (ONOS, OpenDaylight, Ryu)};
\node[layer, fill=green!15] (inf) at (0, 0) {Infrastructure Layer\\Switches / Routers (solo data plane)};

\draw[arrow] (app) -- (ctrl) node[midway, right, font=\small] {Northbound API (REST/gRPC)};
\draw[arrow] (ctrl) -- (app);
\draw[arrow] (ctrl) -- (inf) node[midway, right, font=\small] {Southbound API (OpenFlow/NETCONF)};
\draw[arrow] (inf) -- (ctrl);
\end{tikzpicture}
\end{center}

\begin{itemize}
    \item \textbf{Northbound API:} las aplicaciones de negocio le dicen al
          controlador qué quieren (``bloquea tráfico entre VLAN 10 y VLAN 20'').
          Normalmente REST o gRPC.
    \item \textbf{Southbound API:} el controlador programa los switches directamente.
          OpenFlow es el protocolo más común; también se usa NETCONF/YANG, gRPC/gNMI.
\end{itemize}

\section{\eh{jigsaw} OpenFlow Protocol}

\begin{concepto}
\textbf{OpenFlow} define cómo el controlador instala \textbf{flow entries}
en la flow table de cada switch. Un flow entry dice: ``si el paquete coincide
con estas condiciones, haz esta acción''.
\end{concepto}

\begin{verbatim}
  Flow Entry OpenFlow 1.3:
  ┌───────────────────────────────────────────────────────┐
  │ Priority │ Match Fields          │ Actions            │
  ├───────────────────────────────────────────────────────┤
  │ 100      │ ip_src=10.0.1.0/24   │ output: port 3     │
  │          │ ip_dst=10.0.2.0/24   │                    │
  ├───────────────────────────────────────────────────────┤
  │ 50       │ eth_type=0x0806      │ output: controller │
  │          │ (ARP)                │ (send to SDN ctrl) │
  ├───────────────────────────────────────────────────────┤
  │ 0        │ (any)                │ drop               │
  └───────────────────────────────────────────────────────┘

  Match fields disponibles: MAC src/dst, VLAN, IP src/dst,
  protocolo, puerto TCP/UDP, MPLS label, metadata...
\end{verbatim}

\textbf{Pipeline de tablas:} un paquete puede pasar por múltiples flow tables
en secuencia. La tabla 0 hace clasificación, la tabla 1 aplica QoS, la tabla 2
decide el output. Cada tabla puede pasar metadata a la siguiente.

\subsection{Controladores SDN}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{llll}
\toprule
\textbf{Controlador} & \textbf{Lenguaje} & \textbf{Fortaleza} & \textbf{Uso} \\
\midrule
ONOS          & Java    & Telco-grade, HA clustering & Carriers, telcos \\
OpenDaylight  & Java    & Modular, enterprise        & Empresas, Cisco \\
Ryu           & Python  & Simple, académico          & Labs, testing \\
OVS           & C       & Software switch OpenFlow   & Hypervisors, Kubernetes \\
\bottomrule
\end{tabular}
\caption{Controladores SDN}
\end{table}

\section{\eh{brain} Intent-Based Networking (IBN)}

\begin{concepto}
\textbf{IBN} es la evolución de SDN: en vez de programar flow entries
específicas, el administrador declara una \textbf{intención de negocio}
y el sistema la traduce automáticamente a reglas de bajo nivel.

\emoji{light-bulb} \textbf{Analogía:} SDN clásico = le dices al GPS
``toma la Autopista del Sol, luego la 85-D, luego gira en el km 32''.
IBN = le dices ``llévame a la playa más cercana'' y el GPS elige la ruta.
\end{concepto}

Ejemplo de intención:
\begin{verbatim}
  Intención declarada:
    "Los servidores de producción no pueden comunicarse con
     los de desarrollo bajo ninguna circunstancia."

  IBN traduce a:
    → 47 flow entries en 12 switches diferentes
    → ACLs actualizadas en 3 firewalls
    → Políticas de routing ajustadas
    → Todo en segundos, automáticamente
\end{verbatim}

\begin{moderno}
\textbf{\emoji{rocket} Cisco DNA Center y VMware NSX:} los dos productos de
IBN más adoptados. NSX virtualiza toda la red sobre hypervisors (VMware/KVM)
--- cada VM tiene su propia política de micro-segmentación sin tocar el
hardware físico. Cisco DNA Center usa ML para detectar anomalías y auto-remediar.
\end{moderno}

\begin{cuidado}
\textbf{SDN y el Single Point of Failure:} si el controlador cae, los switches
en muchas implementaciones siguen los flows ya instalados (operan con la última
configuración conocida). Pero no pueden aprender nuevas rutas ni adaptarse
a cambios de topología. Controladores de producción (ONOS) se despliegan
en cluster de 3+ nodos para alta disponibilidad.
\end{cuidado}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/03_sdn_openflow.tex
git commit -m "docs: parte2 cap 3 - SDN, OpenFlow flow entries, controladores, IBN"
git push
```

---

## Task 5: Cap 04 — Datacenter: VxLAN + EVPN

**Files:**
- Modify: `chapters_parte2/04_datacenter_vxlan_evpn.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{building-construction} Datacenter --- VxLAN y EVPN}

\begin{concepto}
Un datacenter moderno tiene decenas de miles de servidores. Las VLANs del
Part 1 tienen un límite de 4094 y no escalan a ese tamaño. Además, Spanning
Tree Protocol (STP) bloquea links para evitar loops --- en un datacenter,
bloquear links es desperdiciar capacidad cara.

\emoji{light-bulb} \textbf{Analogía:} VLANs en datacenter es como intentar
organizar una ciudad de 10 millones de personas con un sistema de numeración
que solo permite 4094 direcciones. VxLAN añade un código postal de 24 bits:
16 millones de ``ciudades'' posibles.
\end{concepto}

\section{\eh{cityscape} Spine-Leaf --- La Topología del Datacenter Moderno}

\begin{concepto}
El datacenter tradicional tenía 3 capas: Core → Distribution → Access.
STP bloqueaba la mitad de los links para evitar loops. El datacenter moderno
usa \textbf{Spine-Leaf}: solo 2 capas, todos los links activos.
\end{concepto}

\begin{center}
\begin{tikzpicture}[
    switch/.style={rectangle, draw, thick, fill=blue!20, minimum width=2.2cm,
                   minimum height=0.7cm, font=\small\bfseries},
    server/.style={rectangle, draw, thick, fill=green!20, minimum width=1.5cm,
                   minimum height=0.5cm, font=\tiny}
]
% Spine switches
\node[switch] (s1) at (1.5, 3) {Spine 1};
\node[switch] (s2) at (4.5, 3) {Spine 2};
\node[switch] (s3) at (7.5, 3) {Spine 3};

% Leaf switches (VTEPs)
\node[switch, fill=orange!20] (l1) at (0, 1) {Leaf 1\\(VTEP)};
\node[switch, fill=orange!20] (l2) at (3, 1) {Leaf 2\\(VTEP)};
\node[switch, fill=orange!20] (l3) at (6, 1) {Leaf 3\\(VTEP)};
\node[switch, fill=orange!20] (l4) at (9, 1) {Leaf 4\\(VTEP)};

% Connections: each leaf → all spines
\foreach \l in {l1,l2,l3,l4} {
    \foreach \s in {s1,s2,s3} {
        \draw[thick] (\l) -- (\s);
    }
}

% Servers under each leaf
\foreach \i/\x in {1/0, 2/3, 3/6, 4/9} {
    \node[server] at (\x-0.5, -0.2) {Server};
    \node[server] at (\x+0.5, -0.2) {Server};
}
\end{tikzpicture}
\end{center}

Propiedades clave:
\begin{itemize}
    \item Cada Leaf conecta con \textbf{todos} los Spines (full mesh entre capas)
    \item \textbf{Sin STP}: el routing usa ECMP (Equal-Cost Multi-Path) --- todos
          los paths están activos y balancean carga
    \item Latencia predecible: máximo \textbf{2 hops} entre cualquier par de servidores
    \item Escala horizontal: agregar un Spine o un Leaf sin rediseñar la red
\end{itemize}

\section{\eh{package} VxLAN --- Virtual Extensible LAN (RFC 7348)}

\begin{concepto}
\textbf{VxLAN} encapsula frames Ethernet completos dentro de paquetes UDP/IP.
La red física (underlay) es L3 pura; la red virtual de los tenants (overlay)
es L2 extendida sobre ella.
\end{concepto}

\textbf{Componentes VxLAN:}
\begin{itemize}
    \item \textbf{VNI} (VxLAN Network Identifier): 24 bits → 16,777,216 segmentos
          (vs 4094 de VLANs). Cada tenant tiene su propio VNI.
    \item \textbf{VTEP} (VxLAN Tunnel Endpoint): el dispositivo que encapsula
          frames del tenant en UDP y los desencapsula al llegar. Típicamente el
          Leaf switch o el hypervisor (OVS en Linux/KVM).
    \item \textbf{Puerto UDP: 4789}
\end{itemize}

\begin{verbatim}
  Frame VxLAN encapsulado:

  [ Outer Eth | Outer IP (VTEP→VTEP) | UDP dst:4789 | VxLAN Header | Inner Eth Frame ]
                                                         ^VNI 24bits
                                                         Inner frame: tráfico del tenant
                                                         (con su VLAN, sus MACs, sus IPs)
\end{verbatim}

\begin{ejemplo}
VM-A (en Leaf 1) quiere hablar con VM-B (en Leaf 3), mismo tenant VNI 5000:
\begin{enumerate}
    \item VM-A genera frame Ethernet normal con MAC destino de VM-B
    \item VTEP de Leaf 1 encapsula: IP outer src=10.0.0.1 (Leaf1), dst=10.0.0.3 (Leaf3), VNI=5000
    \item El frame viaja por la red IP underlay (Spine-Leaf, ECMP)
    \item VTEP de Leaf 3 desencapsula, entrega el frame original a VM-B
    \item VM-A y VM-B ``creen'' estar en la misma LAN aunque estén en racks distintos
\end{enumerate}
\end{ejemplo}

\section{\eh{brain} EVPN --- Ethernet VPN (RFC 7432)}

\begin{concepto}
VxLAN sin control plane usa \textbf{flood-and-learn}: cuando no sabe dónde está
una MAC, la floodea a todos los VTEPs. Con 10,000 VMs, eso es mucho tráfico
inútil.

\textbf{EVPN} usa \textbf{BGP} como control plane de VxLAN. Los VTEPs
anuncian sus MACs/IPs por BGP. Cuando Leaf 1 necesita llegar a VM-B,
ya sabe por BGP en qué VTEP está --- sin flooding.
\end{concepto}

\subsection{Route Types EVPN principales}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Type} & \textbf{Nombre} & \textbf{Qué anuncia} \\
\midrule
Type 2 & MAC/IP Advertisement & ``VM con MAC aa:bb:cc y IP 10.0.1.5 está en mi VTEP'' \\
Type 3 & Inclusive Multicast  & ``Únete a mi árbol multicast para BUM traffic'' \\
Type 5 & IP Prefix Route      & ``Prefijo IP externo alcanzable vía mi VTEP'' \\
\bottomrule
\end{tabular}
\caption{EVPN Route Types principales}
\end{table}

\begin{moderno}
\textbf{\emoji{rocket} VxLAN + EVPN en producción:} AWS usa VxLAN internamente
en sus datacenters. Cisco ACI, VMware NSX, y Arista EOS implementan
VxLAN+EVPN. El datacenter de cualquier nube pública grande funciona sobre
este stack: Spine-Leaf físico + VxLAN overlay + BGP EVPN como control plane.
\end{moderno}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/04_datacenter_vxlan_evpn.tex
git commit -m "docs: parte2 cap 4 - Spine-Leaf, VxLAN VTEP/VNI, EVPN BGP route types"
git push
```

---

## Task 6: Cap 05 — MPLS + QoS

**Files:**
- Modify: `chapters_parte2/05_mpls_qos.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{racing-car} MPLS y QoS --- Backbone y Calidad de Servicio}

\begin{concepto}
El internet que ves en tu casa llega a través de la red de un carrier
(Telmex, AT\&T, Telcel). Esa red interior del carrier usa \textbf{MPLS}
para enrutar tráfico de millones de clientes con alta velocidad y garantías
de calidad. \textbf{QoS} asegura que tu llamada de VoIP no se degrada
cuando alguien descarga un torrent en el mismo enlace.
\end{concepto}

\section{\eh{label} MPLS --- Multiprotocol Label Switching}

\begin{concepto}
En IP normal, cada router hace un \textbf{longest prefix match} en su tabla
de routing para cada paquete: busca en miles de entradas, encuentra la más
específica, lo reenvía. Esto toma tiempo --- especialmente a 100 Gbps.

\textbf{MPLS} añade una etiqueta de 32 bits entre el header L2 y L3. Los
routers intermedios hacen \textbf{label lookup}: buscan la etiqueta en una
tabla pequeña y rápida, la intercambian, y reenvían. Mucho más rápido.

\emoji{light-bulb} \textbf{Analogía:} IP es como leer el nombre completo
en cada parada de correo. MPLS es poner un código de barras al paquete:
cada estación solo escanea el código, sin leer la dirección.
\end{concepto}

\subsection{Componentes MPLS}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Componente} & \textbf{Nombre completo} & \textbf{Función} \\
\midrule
LER & Label Edge Router & Agrega (push) y quita (pop) labels en el borde \\
LSR & Label Switch Router & Solo intercambia (swap) labels, no lee IP \\
LSP & Label Switched Path & Camino predeterminado de labels para un flujo \\
FEC & Forwarding Equiv. Class & Grupo de paquetes que reciben mismo tratamiento \\
\bottomrule
\end{tabular}
\caption{Componentes MPLS}
\end{table}

\subsection{Formato del label MPLS}

\begin{verbatim}
  Label MPLS (32 bits, entre headers L2 y L3):

  0                   1                   2                   3
  0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
  +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
  |                Label (20 bits)                |TC |S|   TTL   |
  +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

  Label: 20 bits, el identificador del path (0-1048575)
  TC: 3 bits, Traffic Class (para QoS)
  S: 1 bit, Bottom of Stack (1 = última label en el stack)
  TTL: 8 bits, como en IP
\end{verbatim}

\subsection{LDP vs RSVP-TE}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Característica} & \textbf{LDP} & \textbf{RSVP-TE} \\
\midrule
Propósito     & Distribución automática de labels & Traffic Engineering \\
Path selection & Sigue IGP (OSPF/IS-IS)           & Explícitamente configurado \\
Reserva BW    & \emoji{cross-mark} No              & \emoji{check-mark-button} Sí \\
Complejidad   & Baja                               & Alta \\
Uso           & MPLS básico                        & Garantías de ancho de banda \\
\bottomrule
\end{tabular}
\caption{LDP vs RSVP-TE}
\end{table}

\subsection{MPLS VPN}

\begin{itemize}
    \item \textbf{L3VPN (RFC 4364):} el carrier enruta tráfico IP del cliente.
          Cada cliente tiene su propio \textbf{VRF} (Virtual Routing and Forwarding)
          --- tabla de routing aislada. El cliente ve una WAN privada transparente.
    \item \textbf{L2VPN / VPLS:} el carrier transporta frames Ethernet del cliente.
          El cliente maneja su propio routing; el carrier solo transporta L2.
          Útil cuando el cliente quiere extender su LAN entre sitios.
\end{itemize}

\section{\eh{bar-chart} QoS --- Quality of Service}

\begin{concepto}
Un enlace de 1 Gbps no distingue entre una llamada de VoIP (pequeños paquetes,
ultra-sensibles a latencia) y una descarga de backup (paquetes grandes,
insensible a latencia). Sin QoS, el backup puede causar jitter en la llamada.

\emoji{light-bulb} \textbf{Analogía:} el aeropuerto sin QoS = una sola fila
para todos. Con QoS = fila de Primera Clase, fila de negocios, fila de turista.
VoIP viaja en Primera, el backup va en turista.
\end{concepto}

\subsection{DSCP --- Differentiated Services Code Point}

DSCP usa 6 bits del campo DS del header IP (reemplaza el antiguo ToS).
$2^6 = 64$ clases posibles:

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{llll}
\toprule
\textbf{DSCP} & \textbf{Nombre} & \textbf{Decimal} & \textbf{Uso} \\
\midrule
EF     & Expedited Forwarding  & 46 & VoIP, videoconferencia \\
AF41   & Assured Forwarding 4-1 & 34 & Video streaming \\
AF21   & Assured Forwarding 2-1 & 18 & Datos críticos \\
CS0/BE & Best Effort           & 0  & Tráfico normal (default) \\
\bottomrule
\end{tabular}
\caption{Clases DSCP comunes}
\end{table}

\subsection{Mecanismos de QoS}

\begin{enumerate}
    \item \textbf{Classification \& Marking:} identificar tráfico en el ingreso
          y asignar DSCP. Mejor hacerlo cerca del origen.
    \item \textbf{Queuing (CBWFQ):} Class-Based Weighted Fair Queuing --- múltiples
          colas, cada clase garantiza un porcentaje del ancho de banda.
    \item \textbf{LLQ} (Low Latency Queuing): cola de prioridad estricta para VoIP.
          Se sirve primero, siempre, antes que cualquier otra cola.
    \item \textbf{WRED} (Weighted Random Early Detection): empieza a descartar
          paquetes de baja prioridad \textit{antes} de que la cola se llene.
          TCP reacciona reduciendo velocidad. Evita tail-drop total.
    \item \textbf{Policing vs Shaping:}
          \begin{itemize}
              \item Policing: si el tráfico excede el límite → \textbf{descarta} el exceso (brusco)
              \item Shaping: si el tráfico excede el límite → \textbf{bufferiza} el exceso (suave)
          \end{itemize}
\end{enumerate}

\begin{ejemplo}
Diseño QoS para una sucursal con enlace de 10 Mbps:
\begin{verbatim}
  Cola LLQ (VoIP, DSCP EF):        2 Mbps garantizados, prioridad estricta
  Cola CBWFQ-1 (Video, DSCP AF41): 4 Mbps garantizados
  Cola CBWFQ-2 (Datos críticos):   2 Mbps garantizados
  Cola Best Effort:                 2 Mbps (el resto)
  Total: 10 Mbps, VoIP nunca espera
\end{verbatim}
\end{ejemplo}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/05_mpls_qos.tex
git commit -m "docs: parte2 cap 5 - MPLS labels/LSP/LDP/RSVP-TE, MPLS VPN, QoS DSCP, LLQ, WRED"
git push
```

---

## Task 7: Cap 06 — Kubernetes Networking

**Files:**
- Modify: `chapters_parte2/06_kubernetes_networking.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{ship} Kubernetes Networking}

\begin{concepto}
Kubernetes (K8s) es el orquestador de contenedores dominante. Cada aplicación
corre en \textbf{Pods} (uno o más contenedores). El networking de K8s tiene
reglas propias que no existen en la red tradicional.

\emoji{light-bulb} \textbf{Analogía:} K8s es como una ciudad donde cada
edificio (Pod) tiene su propia dirección única (IP), sin importar en qué
manzana (Node) esté construido. Y hay un servicio de correo (Services) que
sabe encontrar cualquier edificio aunque se mude.
\end{concepto}

\section{\eh{globe-with-meridians} El Modelo de Red de Kubernetes}

Tres reglas fundamentales que todo el networking de K8s debe respetar:
\begin{enumerate}
    \item \textbf{Pod-to-Pod:} todos los Pods pueden comunicarse entre sí
          directamente con su IP, sin NAT. Un Pod en Node A habla directamente
          con un Pod en Node B usando IPs de Pod.
    \item \textbf{Node-to-Pod:} los Nodes pueden hablar con todos los Pods
          directamente.
    \item \textbf{Pod IP = la IP que el Pod ve en sí mismo:} no hay DNAT oculto.
\end{enumerate}

Cada Pod tiene su propia IP tomada del \textbf{Pod CIDR} del cluster
(ej. 10.244.0.0/16). Los Pods en Node 1 usan 10.244.1.0/24, los de Node 2
usan 10.244.2.0/24, etc.

\section{\eh{electric-plug} CNI --- Container Network Interface}

\begin{concepto}
\textbf{CNI} es la especificación que define cómo un plugin de red configura
el networking de cada Pod cuando arranca. K8s llama al plugin CNI y este
conecta el Pod a la red.

Distintos plugins implementan el modelo de red de K8s de maneras diferentes:
overlay (VxLAN), routing directo (BGP), o eBPF.
\end{concepto}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{lllll}
\toprule
\textbf{Plugin} & \textbf{Mecanismo} & \textbf{NetworkPolicy} & \textbf{Performance} & \textbf{Nota} \\
\midrule
Flannel  & VxLAN overlay  & \emoji{cross-mark} No   & Mediano    & Simple, fácil \\
Calico   & BGP routing    & \emoji{check-mark-button} Sí & Alto  & Más usado en prod \\
Cilium   & eBPF           & \emoji{check-mark-button} L7 & Muy alto & Reemplaza kube-proxy \\
Weave    & Mesh overlay   & \emoji{check-mark-button} Sí & Mediano  & Cifrado integrado \\
\bottomrule
\end{tabular}
\caption{CNI Plugins comparados}
\end{table}

\begin{moderno}
\textbf{\emoji{rocket} Cilium y eBPF:} eBPF (extended Berkeley Packet Filter)
permite ejecutar código en el kernel de Linux sin modificarlo. Cilium usa eBPF
para bypasear iptables completamente --- las reglas de red se ejecutan directamente
en el kernel, más rápido y con observability nativa. Google GKE Dataplane V2,
Meta, y Cloudflare usan Cilium en producción.
\end{moderno}

\section{\eh{mailbox-with-mail} Services --- Cómo se Expone una App}

\begin{concepto}
Los Pods son efímeros: mueren y se recrean con nuevas IPs. Un \textbf{Service}
es una IP virtual estable que balancea carga hacia los Pods activos con un
determinado label.
\end{concepto}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Tipo} & \textbf{Alcance} & \textbf{Uso} \\
\midrule
ClusterIP    & Solo dentro del cluster    & Comunicación inter-servicio \\
NodePort     & IP del Node + puerto alto  & Exposición básica (dev/testing) \\
LoadBalancer & IP externa (cloud LB)      & Producción en nube pública \\
ExternalName & Alias DNS externo          & Integrar servicios externos \\
\bottomrule
\end{tabular}
\caption{Tipos de Service en Kubernetes}
\end{table}

\subsection{kube-proxy}

\textbf{kube-proxy} corre en cada Node y programa reglas iptables (o eBPF)
para implementar los Services. Cuando un Pod envía tráfico a la ClusterIP de
un Service, kube-proxy redirige el paquete a uno de los Pods de ese Service
(round-robin por defecto).

\begin{verbatim}
  Pod A → ClusterIP 10.96.0.10:80
  kube-proxy (iptables DNAT):
    10.96.0.10:80 → 10.244.1.5:8080  (Pod Backend-1)
    10.96.0.10:80 → 10.244.2.3:8080  (Pod Backend-2)
    10.96.0.10:80 → 10.244.3.7:8080  (Pod Backend-3)
    (round-robin, stateless)
\end{verbatim}

\section{\eh{right-arrow-curving-up} Ingress --- L7 Routing}

\begin{concepto}
\textbf{Ingress} permite un solo Load Balancer externo para múltiples Services,
con routing basado en path o hostname (L7). Sin Ingress, cada Service
LoadBalancer necesita su propia IP externa --- costoso en cloud.
\end{concepto}

\begin{verbatim}
  Ingress:
    api.empresa.com/v1     → Service: api-v1
    api.empresa.com/v2     → Service: api-v2
    admin.empresa.com      → Service: admin-dashboard

  Ingress Controllers: nginx-ingress, Traefik, AWS ALB Controller
\end{verbatim}

\section{\eh{no-entry} NetworkPolicy --- Firewall a Nivel Pod}

Por defecto en K8s: \textbf{todo tráfico entre Pods está permitido}.
\textbf{NetworkPolicy} define reglas de ingress/egress a nivel Pod usando
selectors de labels.

\begin{codigo}
\begin{lstlisting}
# Política: solo los Pods con label "app: frontend"
# pueden acceder al "app: backend" en puerto 8080
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: backend-policy
spec:
  podSelector:
    matchLabels:
      app: backend
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend
    ports:
    - port: 8080
\end{lstlisting}
\end{codigo}

\section{\eh{spider-web} Service Mesh --- Istio}

\begin{concepto}
Un \textbf{Service Mesh} añade un proxy sidecar (Envoy) a cada Pod.
El sidecar intercepta todo el tráfico de entrada y salida del Pod,
sin modificar el código de la aplicación.

Beneficios: mTLS automático, circuit breaking, retries, observability
(métricas, trazas distribuidas, logs de cada request).
\end{concepto}

\begin{verbatim}
  Sin Istio:   Pod A ──HTTP──► Pod B

  Con Istio:   Pod A ──HTTP──► [Envoy sidecar A]
                                   │ mTLS
                              [Envoy sidecar B] ──HTTP──► Pod B

  Los sidecars manejan: TLS, auth, rate limiting, circuit breaking.
  La app no sabe que existe el sidecar.
\end{verbatim}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/06_kubernetes_networking.tex
git commit -m "docs: parte2 cap 6 - K8s Pod model, CNI, Cilium eBPF, Services, Ingress, NetworkPolicy, Istio"
git push
```

---

## Task 8: Cap 07 — Cloud Networking

**Files:**
- Modify: `chapters_parte2/07_cloud_networking.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{cloud} Cloud Networking --- AWS y Azure}

\begin{concepto}
Las nubes públicas (AWS, Azure, GCP) son datacenters gigantes con una capa
de abstracción virtual encima. En vez de comprar switches y routers físicos,
configuras \textbf{redes virtuales} con APIs. Los conceptos son los mismos
(subnets, routing, firewalls), solo cambian los nombres y la forma de configurarlos.

\emoji{light-bulb} \textbf{Analogía:} en red tradicional, tú compras cables
y switches. En cloud, le dices al proveedor ``dame una red con estas características''
y ellos la crean virtualmente en segundos, sobre su infraestructura física.
\end{concepto}

\section{\eh{cloud} AWS VPC --- Virtual Private Cloud}

\begin{concepto}
Una \textbf{VPC} es tu red privada aislada dentro de AWS. Defines el bloque
CIDR (ej. 10.0.0.0/16), y dentro creas subnets, tablas de routing, y firewalls.
Ningún otro cliente de AWS puede ver tu tráfico VPC.
\end{concepto}

\subsection{Componentes principales de una VPC}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{ll}
\toprule
\textbf{Componente} & \textbf{Función} \\
\midrule
VPC                & Red virtual privada, define el bloque CIDR raíz \\
Subnet pública     & Tiene ruta al Internet Gateway → instancias con IP pública \\
Subnet privada     & Sin ruta directa a Internet → instancias no alcanzables desde fuera \\
Internet Gateway   & Conecta la VPC a Internet (stateful, no cobra) \\
NAT Gateway        & Permite a subnets privadas salir a Internet (sin entrada) \\
Security Group     & Firewall stateful a nivel instancia/ENI, solo allow rules \\
NACL               & Firewall stateless a nivel subnet, allow + deny rules \\
Route Table        & Define a dónde va el tráfico de cada subnet \\
VPC Peering        & Conexión directa entre dos VPCs (misma o diferente cuenta/región) \\
Transit Gateway    & Hub central: conecta N VPCs + on-premises (en estrella) \\
Direct Connect     & Enlace físico dedicado AWS $\leftrightarrow$ tu datacenter \\
\bottomrule
\end{tabular}
\caption{Componentes AWS VPC}
\end{table}

\subsection{Arquitectura VPC típica}

\begin{verbatim}
  VPC: 10.0.0.0/16
  │
  ├── Subnet pública 10.0.1.0/24 (AZ us-east-1a)
  │   ├── Load Balancer (IP pública)
  │   └── NAT Gateway
  │
  ├── Subnet privada 10.0.2.0/24 (AZ us-east-1a)
  │   └── EC2 (app servers) ← solo accesible desde el LB
  │
  ├── Subnet privada 10.0.3.0/24 (AZ us-east-1b)
  │   └── RDS (base de datos) ← solo accesible desde app servers
  │
  └── Internet Gateway
      └── Route: 0.0.0.0/0 → IGW (solo en subnets públicas)
\end{verbatim}

\subsection{Security Groups vs NACLs}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Característica} & \textbf{Security Group} & \textbf{NACL} \\
\midrule
Nivel           & Instancia/ENI          & Subnet \\
Estado          & Stateful (rastreo)     & Stateless (sin rastreo) \\
Reglas          & Solo allow             & Allow + Deny \\
Orden           & Todas se evalúan       & Orden numérico (first match) \\
Dirección       & Ingress + Egress       & Ingress + Egress separados \\
\bottomrule
\end{tabular}
\caption{Security Groups vs NACLs en AWS}
\end{table}

\begin{cuidado}
\textbf{NACLs stateless:} si permites tráfico HTTP de entrada en el NACL,
debes también permitir el tráfico de respuesta de salida explícitamente
(puertos efímeros 1024-65535). Security Groups no tienen este problema
porque son stateful: si permite la entrada, automáticamente permite la respuesta.
\end{cuidado}

\section{\eh{cloud} Azure Virtual Network (VNet)}

Azure VNet es el equivalente de AWS VPC. Los conceptos son casi idénticos
con nombres diferentes:

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Concepto} & \textbf{AWS} & \textbf{Azure} \\
\midrule
Red virtual         & VPC                & VNet \\
Firewall instancia  & Security Group     & NSG (Network Security Group) \\
Firewall subnet     & NACL               & NSG (mismo, aplica a subnets también) \\
Conexión VPCs       & VPC Peering        & VNet Peering \\
Hub multi-VNet      & Transit Gateway    & Virtual WAN Hub / Azure Route Server \\
Link privado cloud  & Direct Connect     & ExpressRoute \\
DNS privado         & Route 53 (private) & Azure Private DNS \\
IP pública          & Elastic IP         & Public IP Address \\
\bottomrule
\end{tabular}
\caption{AWS vs Azure: equivalencias de networking}
\end{table}

\begin{ejemplo}
\textbf{Diferencia conceptual importante:} en AWS, las subnets son explícitamente
``públicas'' o ``privadas'' según si tienen una ruta al Internet Gateway. En Azure,
todas las subnets pueden tener o no acceso a Internet según el NSG y la tabla de
rutas. No hay una distinción de ``tipo'' en la subnet misma.
\end{ejemplo}

\begin{moderno}
\textbf{\emoji{rocket} AWS Transit Gateway:} antes de Transit Gateway (2018),
conectar 10 VPCs requería 45 peering connections (malla completa). Transit
Gateway actúa como router central: cada VPC conecta solo con el TGW, y el TGW
enruta entre todas. También puede conectar VPNs y Direct Connect. Soporta
hasta 5,000 VPCs por TGW.
\end{moderno}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/07_cloud_networking.tex
git commit -m "docs: parte2 cap 7 - AWS VPC, subnets, SG vs NACL, Transit Gateway, Azure VNet"
git push
```

---

## Task 9: Cap 08 — Multicast

**Files:**
- Modify: `chapters_parte2/08_multicast.tex`

- [ ] **Step 1: Write the chapter**

```latex
\chapter{\eh{loudspeaker} Multicast --- Distribución Eficiente 1-a-Muchos}

\begin{concepto}
Imagina que quieres transmitir la Champions League a 1 millón de usuarios.
\textbf{Unicast} = 1 millón de streams separados desde el servidor.
\textbf{Multicast} = el servidor envía \textit{uno} solo, y la red lo replica
solo donde hay usuarios interesados.

\emoji{light-bulb} \textbf{Analogía:} unicast es tener un profesor que le explica
lo mismo individualmente a cada alumno. Multicast es una clase con 30 alumnos:
el profesor habla una vez y todos escuchan.
\end{concepto}

\section{\eh{bar-chart} Unicast vs Broadcast vs Multicast vs Anycast}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.4}
\begin{tabular}{lllll}
\toprule
\textbf{Tipo} & \textbf{Destino} & \textbf{Copias} & \textbf{Scope} & \textbf{Uso} \\
\midrule
Unicast   & Un host específico   & 1 por destino     & WAN/LAN  & HTTP, SSH, DNS \\
Broadcast & Todos en la subnet   & 1 (red replica)   & Solo LAN & ARP, DHCP \\
Multicast & Grupo de interesados & 1 (red replica)   & LAN/WAN  & IPTV, VoIP, OSPF \\
Anycast   & El más cercano del grupo & 1             & WAN      & DNS (1.1.1.1), CDN \\
\bottomrule
\end{tabular}
\caption{Tipos de entrega}
\end{table}

\section{\eh{world-map} Direcciones Multicast IPv4}

Las IPs multicast están en el rango \textbf{224.0.0.0/4} (Clase D):

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Rango} & \textbf{Nombre} & \textbf{Uso} \\
\midrule
224.0.0.0/24  & Link-local (RFC 5771)   & Solo en la LAN local (TTL=1). No enrutado. \\
224.0.0.1     & All hosts               & Todos los hosts en la subnet \\
224.0.0.2     & All routers             & Todos los routers en la subnet \\
224.0.0.5     & All OSPF routers        & OSPF hello packets \\
224.0.0.251   & mDNS                    & Bonjour/Avahi (Apple, impresoras) \\
224.0.1.0 -- 238.255.255.255 & Global  & Internet multicast (IANA asignado) \\
232.0.0.0/8   & SSM range               & Source-Specific Multicast \\
239.0.0.0/8   & Admin-scoped            & Multicast privado (como 192.168/16) \\
\bottomrule
\end{tabular}
\caption{Rangos de direcciones multicast IPv4}
\end{table}

\section{\eh{ear} IGMP --- Internet Group Management Protocol}

\begin{concepto}
\textbf{IGMP} es el protocolo entre un host y su router local. El host le dice
al router ``quiero recibir el grupo 239.1.2.3''. El router lo registra y
solicita ese stream hacia arriba en la red multicast.

Sin IGMP, los routers no sabrían qué hosts quieren qué grupos.
\end{concepto}

\subsection{Versiones IGMP}

\begin{table}[h!]
\centering
\renewcommand{\arraystretch}{1.3}
\begin{tabular}{lll}
\toprule
\textbf{Versión} & \textbf{Novedad} & \textbf{Mensajes} \\
\midrule
IGMPv1 & Básico                  & Report, Query \\
IGMPv2 & Leave Group (más rápido) & Report, Query, Leave \\
IGMPv3 & Source-Specific (SSM)   & Report con lista de fuentes permitidas \\
\bottomrule
\end{tabular}
\caption{Versiones IGMP}
\end{table}

\textbf{Proceso IGMP básico:}
\begin{enumerate}
    \item Host envía \textbf{IGMP Membership Report} al grupo 239.1.2.3
    \item Router registra: ``puerto X tiene interés en 239.1.2.3''
    \item Router envía periódicamente \textbf{IGMP Query} al grupo
    \item Hosts responden con Report para mantener el registro activo
    \item Si el host ya no quiere el stream: \textbf{IGMP Leave} (v2/v3)
\end{enumerate}

\section{\eh{deciduous-tree} PIM --- Protocol Independent Multicast}

\begin{concepto}
\textbf{PIM} es el protocolo de routing multicast entre routers. ``Protocol
Independent'' significa que funciona sobre cualquier protocolo de unicast
(OSPF, BGP, IS-IS) sin modificarlo.

PIM construye árboles de distribución: caminos desde la fuente del stream
hasta todos los receptores interesados.
\end{concepto}

\subsection{PIM-SM --- Sparse Mode}

\textbf{PIM-SM} (RFC 7761) es el modo estándar para redes donde los receptores
son dispersos (la mayoría de redes reales):

\begin{enumerate}
    \item \textbf{Rendezvous Point (RP):} router central de encuentro entre fuentes
          y receptores. Todos los routers conocen la IP del RP.
    \item \textbf{Join hacia el RP:} cuando un receptor quiere el grupo G, su router
          envía PIM Join hacia el RP. Se forma el \textbf{RPT} (RP Tree).
    \item \textbf{Fuente se registra:} cuando una fuente envía al grupo G, su DR
          (Designated Router) encapsula el tráfico y lo envía al RP vía unicast
          (PIM Register).
    \item \textbf{RP une fuente y receptores:} el RP desencapsula y envía el
          tráfico por el RPT hacia los receptores.
    \item \textbf{SPT Switchover:} si el tráfico es alto, el router del receptor
          hace Join directamente hacia la fuente (\textbf{SPT}, Shortest Path Tree).
          Más eficiente que pasar por el RP.
\end{enumerate}

\begin{center}
\begin{tikzpicture}[
    router/.style={circle, draw, thick, fill=blue!20, minimum size=1cm, font=\small\bfseries},
    rp/.style={circle, draw, thick, fill=red!30, minimum size=1.2cm, font=\small\bfseries},
    host/.style={rectangle, draw, thick, fill=green!20, minimum size=0.7cm, font=\tiny},
    arr/.style={-{Stealth}, thick}
]
\node[rp] (rp) at (4, 3) {RP};
\node[router] (r1) at (1, 1.5) {R1};
\node[router] (r2) at (4, 1.5) {R2};
\node[router] (r3) at (7, 1.5) {R3};
\node[host] (src) at (1, 0) {Fuente};
\node[host] (rx1) at (4, 0) {Receptor 1};
\node[host] (rx2) at (7, 0) {Receptor 2};

\draw[thick] (rp) -- (r1);
\draw[thick] (rp) -- (r2);
\draw[thick] (rp) -- (r3);
\draw[thick] (r1) -- (src);
\draw[thick] (r2) -- (rx1);
\draw[thick] (r3) -- (rx2);

\draw[arr, red, dashed] (r1) -- (rp) node[midway, left, font=\tiny] {PIM Register};
\draw[arr, blue] (rp) -- (r2) node[midway, right, font=\tiny] {stream};
\draw[arr, blue] (rp) -- (r3);
\end{tikzpicture}
\end{center}

\begin{moderno}
\textbf{\emoji{rocket} Casos de uso reales de multicast:}
\begin{itemize}
    \item \textbf{IPTV (Telmex/Totalplay):} el stream de cada canal de TV se distribuye
          por multicast. Solo los STBs que sintonizaron ese canal reciben el tráfico.
          Sin multicast, el ancho de banda del DSLAM explotaría.
    \item \textbf{Trading financiero:} los feeds de precios de bolsa (NYSE, NASDAQ)
          se distribuyen por multicast a miles de traders simultáneamente.
          Latencia uniforme para todos --- ventaja competitiva crítica.
    \item \textbf{Software distribution en datacenter:} AWS usa multicast internamente
          para distribuir imágenes de sistema a miles de servidores simultáneamente.
\end{itemize}
\end{moderno}

\begin{cuidado}
\textbf{Multicast en Internet público:} el routing multicast entre ASNs
(MBONE) existe técnicamente pero casi ningún ISP lo soporta comercialmente.
En Internet público, el multicast se simula con CDNs (unicast a servidores
edge) y protocolos como HLS/DASH. El multicast real solo funciona dentro
de una red controlada (ISP, datacenter, campus).
\end{cuidado}
```

- [ ] **Step 2: Compile and check**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`

- [ ] **Step 3: Commit**

```bash
git add chapters_parte2/08_multicast.tex
git commit -m "docs: parte2 cap 8 - Unicast/Multicast/Anycast, IGMP, PIM-SM, RP, SPT, casos reales"
git push
```

---

## Task 10: Final — Segundo pass + PDF

- [ ] **Step 1: Segundo pass para ToC correcto**

```bash
cd "D:/Codigo Abierto/RedesDeDatos"
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex
grep -c "^!" ApuntesRedes_Parte2.log
```

Expected: `0`, PDF con ToC completa y numeración correcta.

- [ ] **Step 2: Commit PDF final**

```bash
git add ApuntesRedes_Parte2.pdf
git commit -m "docs: PDF final Parte 2 compilado - todos los capítulos"
git push
```

- [ ] **Step 3: Verificar repo**

```bash
git log --oneline -5
```

Expected: commits de todos los capítulos + PDF visible en GitHub.
