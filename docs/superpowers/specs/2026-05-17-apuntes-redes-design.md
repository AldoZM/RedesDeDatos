# Design Spec: Apuntes de Redes de Datos — LaTeX Study Notes

**Date:** 2026-05-17  
**Author:** Aldo Zepeda (AldoZM)  
**Repo:** https://github.com/AldoZM/RedesDeDatos  
**Source manual:** `MADO-31_LabRedesDatosSeguras.pdf` (479 pages, UNAM Facultad de Ingeniería, 2023)

---

## 1. Objetivo

Crear apuntes de estudio teórico profundo sobre redes de datos y protocolos de comunicación, en formato LaTeX exportable a PDF. Los apuntes:

- Están en **Spanglish técnico** (explicaciones en español, términos técnicos en inglés)
- Usan **muchos emojis** para hacerlos visualmente atractivos
- Explican conceptos con **analogías simples** (nivel 12 años) + **profundidad técnica** (headers, algoritmos, diagramas)
- Cubren el contenido del manual MADO-31 y lo **complementan y actualizan** con tecnologías modernas (2016–2025)
- Se **commitean y pushean** al repo al terminar cada archivo `.tex`

---

## 2. Arquitectura de archivos

```
D:\Codigo Abierto\RedesDeDatos\
├── ApuntesRedes.tex              ← raíz: portada, ToC, \input{} de todos los capítulos
├── chapters/
│   ├── 00_intro.tex              ← ¿Qué es una red? Historia, OSI vs TCP/IP
│   ├── 01_capa1_fisica.tex       ← Capa Física: cables, normas EIA/TIA, fibra, señales
│   ├── 02_capa2_enlace.tex       ← Capa Enlace: MAC, Ethernet, switch, VLAN, STP
│   ├── 03_capa3_red.tex          ← Capa Red: IP, subnetting, routing, IPv6, NAT
│   ├── 04_capa4_transporte.tex   ← Capa Transporte: TCP, UDP, handshake, flags, QUIC
│   ├── 05_capa5_sesion.tex       ← Capa Sesión: SSH, TLS sessions, NetBIOS
│   ├── 06_capa6_presentacion.tex ← Capa Presentación: codificación, cifrado, TLS/SSL
│   ├── 07_capa7_aplicacion.tex   ← Capa Aplicación: DHCP, DNS, HTTP/1.1/2/3, SMTP, FTP
│   ├── 08_modernos_google.tex    ← Protocolos modernos: QUIC, HTTP/3, gRPC, BBR, WireGuard, Wi-Fi 7
│   └── 09_seguridad_redes.tex    ← Seguridad: VPN, firewalls, Zero Trust, ataques, mTLS
├── assets/                       ← imágenes externas (PNG/PDF de diagramas)
├── docs/
│   └── superpowers/specs/
│       └── 2026-05-17-apuntes-redes-design.md
├── MADO-31_LabRedesDatosSeguras.pdf
└── .gitignore                    ← *.aux, *.log, *.out, *.toc + ApuntesRedes.pdf (compilado); el manual PDF sí se versiona
```

**LaTeX engine:** `pdflatex`  
**Paquetes clave:** `babel{spanish}`, `fontawesome5` (emojis/íconos), `tcolorbox`, `listings`, `tikz`, `pgf`, `geometry`, `hyperref`, `inputenc{utf8}`, `fontenc{T1}`

---

## 3. Estructura interna de cada capítulo

Cada `.tex` sigue esta plantilla:

```
\chapter{🔌 Capa X — Nombre} 

\section{🧠 ¿Qué es?}       ← Definición + analogía de 12 años
\section{🔍 ¿Cómo funciona?} ← Teoría profunda, headers, algoritmos
\section{🖼️ Diagrama}        ← TikZ diagram o ASCII art en verbatim
\section{📦 Ejemplo real}    ← Con IPs, capturas simuladas, configuraciones
\section{⚠️ Confusiones comunes} ← Errores conceptuales frecuentes
\section{🔗 Conexión con el modelo OSI} ← Dónde vive, qué capas interactúan
```

**Cajas visuales con `tcolorbox`:**
- Azul claro: `🧠 Concepto`
- Verde: `📦 Ejemplo`
- Naranja: `⚠️ Cuidado / Error común`
- Morado: `🚀 Tecnología moderna`
- Gris: `💻 Configuración / Código`

---

## 4. Contenido por capítulo

### `00_intro.tex`
- Historia: ARPANET → Internet
- ¿Por qué existen los protocolos?
- Modelo OSI (7 capas) con analogía + tabla resumen
- Modelo TCP/IP (4 capas) comparado con OSI
- Organismos de estandarización: IETF, IANA, IEEE, ANSI, ISO
- ¿Qué es un RFC? Tipos y proceso

### `01_capa1_fisica.tex`
(Cubre Prácticas 1–3, Complementarias 2–3)
- Señales analógicas vs digitales
- Cable UTP: pares trenzados, por qué se trenza, interferencia EMI
- Categorías UTP: Cat5e, Cat6, Cat6a, Cat7, Cat8 — velocidades, distancias
- Normas ANSI/EIA/TIA 568-A/B: T568-A vs T568-B, straight-through vs crossover
- Cableado estructurado: 6 subsistemas, patch panel, jack RJ-45
- Fibra óptica: multimodo vs monomodo, conectores LC/SC/ST
- Wi-Fi: 802.11a/b/g/n/ac/ax (Wi-Fi 6) → 802.11be (Wi-Fi 7, 2024)

### `02_capa2_enlace.tex`
(Cubre Prácticas 4, Complementarias 4–6)
- Dirección MAC: estructura, OUI, unicast/multicast/broadcast
- ARP: Address Resolution Protocol, ARP table, Gratuitous ARP
- Ethernet frame: estructura completa (preámbulo, dst, src, type, payload, FCS)
- Hub vs Switch vs Bridge: diferencias fundamentales
- Switch: MAC table, flooding, forwarding, filtering
- VLANs (802.1Q): trunk ports, access ports, trunking protocol
- STP / RSTP: Spanning Tree, por qué existe, cómo elige root bridge
- EtherChannel / LACP: link aggregation
- Port security: MAC limiting, sticky MAC, violation modes

### `03_capa3_red.tex`
(Cubre Prácticas 6–7, Complementarias 7–8)
- IPv4: estructura del header (20 bytes), campos importantes
- Subnetting completo: CIDR, máscaras, cálculo de redes/hosts
- Tabla de ruteo: rutas estáticas vs dinámicas
- Protocolos de routing dinámico: RIP v2, OSPF (áreas, LSA, SPF), BGP (eBGP/iBGP)
- HSRP (Hot Standby Router Protocol): gateway redundante
- NAT/PAT: tipos (estático, dinámico, overload), por qué existe
- ICMP: ping, traceroute, TTL, tipos de mensajes
- IPv6: formato de dirección, tipos (link-local, global, multicast), dual-stack, túneles
- RPKI: BGP security, route origin validation (2023-activo)

### `04_capa4_transporte.tex`
(Cubre Práctica 8, Complementaria 9)
- Puertos: well-known (0-1023), registered, ephemeral
- UDP: connectionless, header de 8 bytes, casos de uso (DNS, streaming, gaming)
- TCP: connection-oriented, header completo (20 bytes), todos los flags
- TCP 3-way handshake: SYN → SYN-ACK → ACK con diagrama
- TCP 4-way termination: FIN → FIN-ACK → FIN → ACK
- Control de flujo: ventana deslizante (sliding window), receive window
- Control de congestión: slow start, congestion avoidance, fast retransmit, CUBIC
- QUIC (preview): por qué TCP tiene limitaciones para HTTP

### `05_capa5_sesion.tex`
(Cubre Práctica 9, Complementaria 10)
- ¿Qué hace la capa de sesión? Establecer, mantener, terminar sesiones
- **Nota aclaratoria:** SSH técnicamente opera en Layer 7 (Application), pero el manual MADO-31 lo clasifica en Layer 5. El capítulo explicará ambas perspectivas para evitar confusión en el examen.
- SSH: key exchange (Diffie-Hellman), autenticación por clave pública, port forwarding
- SSH vs Telnet: por qué Telnet es inseguro
- RPC (Remote Procedure Call): concepto
- NetBIOS, SMB: compartición de archivos en redes locales

### `06_capa6_presentacion.tex`
(Cubre Práctica 10)
- Codificación de caracteres: ASCII, Unicode, UTF-8 vs UTF-16
- Serialización: JSON, XML, Protobuf (Google) — comparativa de tamaño
- Compresión: gzip, Brotli (Google, usado en HTTP/2+)
- Cifrado simétrico: AES-128/256, modos (CBC, GCM)
- Cifrado asimétrico: RSA, ECDSA, Diffie-Hellman
- TLS/SSL: handshake completo, certificados X.509, cadena de confianza
- TLS 1.2 vs TLS 1.3: diferencias en handshake, cipher suites eliminados

### `07_capa7_aplicacion.tex`
(Cubre Práctica 11, Complementarias 12–13)
- DHCP: proceso DORA (Discover, Offer, Request, ACK), lease time, opciones
- DNS: jerarquía (raíz → TLD → authoritative), tipos de registros (A, AAAA, MX, CNAME, TXT, NS, PTR), recursivo vs iterativo
- HTTP/1.0 vs HTTP/1.1: keep-alive, pipelining, problemas de head-of-line blocking
- HTTP/2 (RFC 7540): multiplexing, server push, header compression (HPACK), binary framing
- HTTPS: TLS sobre HTTP, HSTS
- FTP vs SFTP vs SCP: transferencia de archivos
- SMTP, POP3, IMAP: correo electrónico
- Firewall básico: stateful vs stateless, iptables, reglas

### `08_modernos_google.tex`
(Tecnologías 2015–2025, sin cobertura en el manual)
- **SPDY** (Google, 2009–2015): predecesor de HTTP/2, problemas que resolvió
- **HTTP/2** (RFC 7540, 2015): multiplexing, HPACK, server push — diagramas comparativos
- **QUIC** (RFC 9000, 2021): UDP + TLS 1.3 integrado, streams independientes, 0-RTT connection resumption, migración de conexión
- **HTTP/3** (RFC 9114, 2022): HTTP sobre QUIC, elimina head-of-line blocking de TCP
- **gRPC** (Google, 2016): RPC sobre HTTP/2, Protobuf, streaming bidireccional, uso en microservicios
- **BBR Congestion Control** (Google, v1 2016, v3 2023): modelo basado en bandwidth estimation, usado en YouTube
- **DNS over HTTPS — DoH** (RFC 8484, 2018): DNS sobre HTTP/2, privacidad
- **DNS over QUIC — DoQ** (RFC 9250, 2022): DNS más rápido con QUIC
- **WebRTC**: comunicación P2P en tiempo real, ICE/STUN/TURN, SRTP
- **ECH / Encrypted Client Hello** (TLS extension, 2023): oculta el SNI, anti-censura
- **Wi-Fi 7** (802.11be, 2024): Multi-Link Operation (MLO), 320 MHz channels, 46 Gbps teórico
- **BeyondCorp** (Google Zero Trust): sin VPN corporativa, acceso basado en identidad y contexto

### `09_seguridad_redes.tex`
(Complementa Complementaria 11 VPN y 12 Firewall)
- VPN: tipos (site-to-site, remote access), protocolos (IPsec, OpenVPN, WireGuard)
- **WireGuard** (2020, en kernel Linux): comparativa con OpenVPN, 4k líneas de código, criptografía moderna (ChaCha20, Curve25519)
- **mTLS** (Mutual TLS): autenticación bidireccional en microservicios
- **Zero Trust**: principios, BeyondCorp como implementación real
- Firewall: stateful, stateless, next-gen (NGFW), WAF
- Ataques de red comunes: ARP Spoofing/Poisoning, DNS Spoofing, BGP Hijacking, MITM, DoS/DDoS
- **RPKI**: Resource Public Key Infrastructure, defensa contra BGP hijacking
- Conceptos: CIA Triad, least privilege, defense in depth

---

## 5. Estilo de escritura

- **Idioma:** Spanglish técnico. Explicaciones en español, términos técnicos (handshake, packet, frame, etc.) en inglés.
- **Tono:** Como explicarle a un amigo de 12 años que es curioso. Analogías cotidianas obligatorias.
- **Emojis:** Abundantes. Cada sección, cada concepto importante, cada caja.
- **Diagramas:** TikZ inline para topologías y flujos; ASCII art en `\begin{verbatim}` para headers y estructuras de paquetes.
- **Profundidad:** Completa. Incluir números de campos, tamaños en bits/bytes, valores de flags, ejemplos con IPs reales (rangos RFC 5737: 192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24).

---

## 6. Flujo de trabajo Git

- Un commit por archivo `.tex` terminado.
- Mensaje de commit en español, conciso.
- Push inmediato después de cada commit.
- Repo: `https://github.com/AldoZM/RedesDeDatos`
- `.gitignore` excluye archivos de compilación LaTeX (`*.aux`, `*.log`, `*.out`, `*.toc`, `*.pdf` del directorio raíz).

---

## 7. Criterios de éxito

- [ ] Cada capítulo compila sin errores con `pdflatex`
- [ ] El PDF resultante es legible y visualmente atractivo
- [ ] Los emojis renderizan correctamente en el PDF
- [ ] Los diagramas TikZ son claros y precisos
- [ ] Los conceptos del manual MADO-31 están cubiertos y ampliados
- [ ] Los protocolos modernos (QUIC, HTTP/3, gRPC, BBR, WireGuard) están explicados con profundidad
- [ ] Todos los archivos están commiteados y pusheados al repo
