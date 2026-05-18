# Apuntes Redes de Datos — Parte 2 (Nivel Senior) Design Spec

> **For agentic workers:** Use superpowers:subagent-driven-development or superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create a second LaTeX document (ApuntesRedes_Parte2.tex) continuing from Part 1, covering senior/infrastructure-level networking topics in the same style.

**Architecture:** Separate root file + separate chapters folder (chapters_parte2/) inside the same repo. Same preamble, same custom environments, same compilation pipeline (LuaLaTeX + Segoe UI Emoji). Part 1 root file gets renamed from ApuntesRedes.tex to ApuntesRedes_Parte1.tex.

**Tech Stack:** LuaLaTeX, emoji package (Segoe UI Emoji), tcolorbox, TikZ, listings, babel{spanish}, booktabs. Same as Part 1.

**Repo:** https://github.com/AldoZM/RedesDeDatos

---

## Style Guidelines (identical to Part 1)

- Spanglish técnico: explanations in Spanish, technical terms in English
- Analogías nivel 12 años + depth técnico real
- `\eh{}` macro for emojis in headings (avoids MakeUppercase bug)
- Custom environments: `concepto` (blue), `ejemplo` (green), `cuidado` (orange), `moderno` (violet), `codigo` (gray)
- TikZ diagrams for topologies and flows
- verbatim blocks for packet formats and CLI output
- Commit + push after each chapter completes
- Compile with: `rm -f *.aux *.log *.out *.toc && lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex`

---

## File Structure

```
RedesDeDatos/
├── ApuntesRedes_Parte1.tex         ← renamed from ApuntesRedes.tex
├── ApuntesRedes_Parte1.pdf         ← renamed from ApuntesRedes.pdf
├── ApuntesRedes_Parte2.tex         ← new root file
├── ApuntesRedes_Parte2.pdf         ← compiled output (tracked in git)
├── chapters/                       ← Part 1 chapters (unchanged)
│   └── 00_intro.tex ... 09_seguridad_redes.tex
├── chapters_parte2/                ← Part 2 chapters (new)
│   ├── 00_intro_p2.tex
│   ├── 01_wireless_empresarial.tex
│   ├── 02_switching_avanzado.tex
│   ├── 03_sdn_openflow.tex
│   ├── 04_datacenter_vxlan_evpn.tex
│   ├── 05_mpls_qos.tex
│   ├── 06_kubernetes_networking.tex
│   ├── 07_cloud_networking.tex
│   └── 08_multicast.tex
└── assets/
```

---

## Chapter Content Spec

### Cap 00 — Intro Parte 2

- Conexión con Part 1: qué ya sabemos, qué nos falta
- Stack del datacenter moderno (diagrama TikZ): Internet → Edge → Spine-Leaf → Servers
- Mapa de tecnologías del documento: dónde vive cada protocolo
- Tabla: Part 1 vs Part 2 scope

### Cap 01 — Wireless Empresarial

**WPA3:**
- WPA2 vs WPA3: SAE (Simultaneous Authentication of Equals) reemplaza PSK
- Forward secrecy en WPA3: cada sesión tiene clave única
- WPA3-Enterprise vs WPA3-Personal
- KRACK attack (WPA2) y por qué WPA3 lo resuelve

**802.1X / EAP:**
- Port-based Network Access Control
- Tres actores: Supplicant (cliente), Authenticator (switch/AP), Authentication Server (RADIUS)
- EAP types tabla: EAP-TLS (certificado cliente), PEAP (contraseña en túnel TLS), EAP-TTLS
- RADIUS protocol: UDP 1812/1813, shared secret, Access-Request/Accept/Reject

**Diagrama TikZ:** flujo 802.1X desde laptop → switch → RADIUS → AD/LDAP

### Cap 02 — Switching Avanzado

**MSTP (802.1s):**
- Problema con RSTP: una instancia STP para todas las VLANs → subóptimo
- MSTP mapea grupos de VLANs a instancias STP independientes
- Configuración: MST region, revision number, instance mapping
- Diagrama: VLAN 10-20 por un path, VLAN 30-40 por otro

**MACsec (802.1AE):**
- Cifrado hop-by-hop en Layer 2 (entre switches adyacentes)
- MKA (MACsec Key Agreement) para intercambio de claves
- Diferencia con TLS: TLS cifra end-to-end, MACsec cifra cada enlace físico
- Overhead: 32 bytes por frame, latencia mínima

**QinQ (802.1ad) — Double Tagging:**
- Problema: cliente tiene VLANs 1-4094, carrier también tiene VLANs → colisión
- QinQ añade segundo tag (S-Tag del carrier, C-Tag del cliente)
- Verbatim: formato del frame con doble tag
- Caso de uso: ISP transporta múltiples clientes con VLANs propias

**Private VLANs:**
- Tipos de puertos: Promiscuous (habla con todos), Isolated (solo habla con Promiscuous), Community (habla con su comunidad + Promiscuous)
- Caso de uso: hosting — cada VM está aislada, solo el router (Promiscuous) las conecta a Internet

**IGMP Snooping:**
- Sin IGMP Snooping: switch floodea tráfico multicast a todos los puertos
- Con IGMP Snooping: switch escucha IGMP Join/Leave y construye tabla de puertos interesados
- Resultado: multicast solo va a puertos que lo pidieron

**Storm Control:**
- Broadcast/multicast/unicast storm: un loop o dispositivo defectuoso genera tráfico exponencial
- Storm Control: umbral en % de ancho de banda o pps → shutdown o drop
- Diferencia con STP: STP previene loops, Storm Control limita el daño si ocurren

**802.1X en switches (wired NAC):**
- Mismo protocolo que Wi-Fi empresarial, aplicado a puertos físicos
- Puerto en estado unauthorized hasta que el cliente autentica
- MAB (MAC Authentication Bypass): dispositivos sin supplicant (impresoras) autentican por MAC

### Cap 03 — SDN + OpenFlow

**Problema del networking tradicional:**
- Control plane (decisiones de routing) y data plane (forwarding) acoplados en el mismo dispositivo
- Cambiar comportamiento → reconfigurar cada switch individualmente
- No hay visibilidad global de la red

**SDN Architecture:**
- Application Layer → Control Layer (SDN Controller) → Infrastructure Layer (switches/routers)
- Northbound API: aplicaciones hablan con el controlador (REST)
- Southbound API: controlador habla con dispositivos (OpenFlow, NETCONF, gRPC)
- Diagrama TikZ: tres capas SDN

**OpenFlow Protocol:**
- Controlador instala flow entries en la flow table de cada switch
- Flow entry: match (campos del paquete) + actions (forward, drop, modify, send-to-controller)
- Pipeline de tablas: paquete pasa por múltiples tablas en secuencia
- Verbatim: formato de flow entry OpenFlow 1.3

**Controladores SDN:**
- ONOS (Open Network Operating System): telco-grade, clustering
- OpenDaylight: enterprise, modular
- Ryu: Python, académico/testing
- OVS (Open vSwitch): implementación software del switch OpenFlow

**Intent-Based Networking (IBN):**
- Evolución de SDN: el admin declara intención ("VMs de producción no hablan con las de dev")
- El controlador traduce la intención a reglas de bajo nivel
- Cisco DNA Center, VMware NSX como ejemplos

### Cap 04 — Datacenter: VxLAN + EVPN

**Limitaciones de VLANs en datacenter:**
- 4094 VLANs máximo → insuficiente para cloud pública con millones de tenants
- STP no escala en redes con miles de switches
- VMs migran entre servidores físicos → necesitan misma L2 sin importar ubicación física

**VxLAN (Virtual Extensible LAN):**
- Overlay L2 sobre red L3 (encapsula frames Ethernet en UDP)
- VNI (VxLAN Network Identifier): 24 bits → 16 millones de segmentos
- VTEP (VxLAN Tunnel Endpoint): el dispositivo que encapsula/desencapsula
- Puerto UDP: 4789
- Verbatim: formato del frame VxLAN (outer Ethernet + IP + UDP + VxLAN header + inner Ethernet)

**Spine-Leaf Topology:**
- Tradicional: Core → Distribution → Access (3 capas, STP bloqueando links)
- Spine-Leaf: todos los leaf conectan a todos los spines (2 capas, ECMP, sin STP)
- Diagrama TikZ: spine-leaf con VTEPs en leaf switches
- Latencia predecible: máximo 2 hops entre cualquier par de servidores

**EVPN como control plane de VxLAN:**
- VxLAN sin EVPN: flood-and-learn (ineficiente, no escala)
- EVPN usa BGP para distribuir información MAC/IP entre VTEPs
- Route Types principales:
  - Type 2: MAC/IP advertisement (aprendizaje de MACs)
  - Type 3: Inclusive Multicast Route (registro para BUM traffic)
- Resultado: VTEPs saben exactamente a qué VTEP enviar sin flooding

### Cap 05 — MPLS + QoS

**MPLS (Multiprotocol Label Switching):**
- En vez de lookup de IP en cada router (lento), se añade etiqueta de 32 bits
- Label Edge Router (LER): agrega/quita labels en el borde
- Label Switch Router (LSR): forwarda basado en label (rápido)
- LSP (Label Switched Path): el camino predeterminado para un flujo
- Verbatim: formato de label MPLS (20 bits label, 3 TC, 1 S, 8 TTL)

**LDP vs RSVP-TE:**
- LDP: distribuye labels automáticamente siguiendo la topología IGP
- RSVP-TE: reserva recursos (bandwidth) a lo largo de un LSP específico → Traffic Engineering

**MPLS VPN:**
- L3VPN: conecta sitios de una empresa sobre backbone del carrier (VRF por cliente)
- L2VPN/VPLS: el carrier transporta L2 del cliente (cliente maneja su propio routing)

**QoS — Quality of Service:**
- Problema: video, VoIP y bulk data compiten por el mismo enlace
- DSCP (Differentiated Services Code Point): 6 bits en el header IP → 64 clases
- Classes comunes: EF (Expedited Forwarding) para VoIP, AF (Assured Forwarding) para video, BE (Best Effort) para web

**Mecanismos de QoS:**
- Classification & Marking: identificar y marcar tráfico en el ingreso
- Queuing (CBWFQ): múltiples colas con bandwidth garantizado por clase
- LLQ (Low Latency Queuing): cola de prioridad estricta para VoIP
- WRED (Weighted Random Early Detection): descarte selectivo antes de que la cola se llene
- Policing: limita tráfico, descarta exceso
- Shaping: limita tráfico, bufferiza exceso (más suave)

### Cap 06 — Kubernetes Networking

**El modelo de red de Kubernetes:**
- Regla fundamental: cada Pod tiene su propia IP, alcanzable desde cualquier otro Pod (sin NAT)
- Flat network entre Pods (aunque estén en diferentes Nodes)
- CNI (Container Network Interface): plugin que implementa este modelo

**CNI Plugins:**
- Flannel: overlay simple (VxLAN o host-gw), fácil, poco features
- Calico: BGP nativo para routing de Pods, NetworkPolicy rico, alto rendimiento
- Cilium: basado en eBPF (bypassa iptables), L7-aware, observability integrada
- Weave: mesh overlay, cifrado entre nodos
- Tabla comparativa: performance, features, complejidad

**kube-proxy:**
- Implementa Services en el Node
- Modo iptables: reglas iptables para balancear tráfico al Service
- Modo eBPF (Cilium/kube-proxy replacement): sin iptables, más rápido

**Services en Kubernetes:**
- ClusterIP: IP virtual interna del cluster (solo accesible dentro)
- NodePort: expone en puerto alto de cada Node
- LoadBalancer: provisiona LB externo (AWS ELB, GCP LB)
- ExternalName: alias DNS a servicio externo

**Ingress:**
- L7 routing: un solo LB externo → múltiples Services basado en path/hostname
- Ingress Controller: nginx, Traefik, AWS ALB Ingress
- Diagrama: Internet → Ingress → Services → Pods

**NetworkPolicy:**
- Firewall a nivel Pod: qué Pods pueden hablar con qué Pods
- Por default: todo abierto (si no hay NetworkPolicy)
- Requiere CNI que lo soporte (Calico, Cilium)

**Service Mesh (Istio):**
- Sidecar proxy (Envoy) en cada Pod → intercept todo el tráfico
- mTLS automático entre servicios sin cambiar código
- Observability: métricas, trazas distribuidas, circuit breaking

### Cap 07 — Cloud Networking

**AWS VPC:**
- VPC: red virtual privada aislada (CIDR propio, ej. 10.0.0.0/16)
- Subnets: public (con ruta a IGW) vs private (sin ruta directa a Internet)
- Internet Gateway (IGW): conecta VPC a Internet
- NAT Gateway: permite que subnets privadas salgan a Internet sin ser alcanzables desde fuera
- Security Groups: stateful firewall a nivel instancia (allow-only)
- NACLs: stateless firewall a nivel subnet (allow + deny)
- VPC Peering: conecta dos VPCs (mismo o diferente account/region)
- Transit Gateway: hub central para conectar múltiples VPCs y on-premises
- Direct Connect: enlace físico dedicado AWS ↔ datacenter (no pasa por Internet)
- Route Tables: controlan a dónde va el tráfico de cada subnet

**Azure VNet:**
- VNet: equivalente a VPC (CIDR propio)
- Subnets: sin distinción public/private en Azure (el routing lo determina)
- NSG (Network Security Group): equivalente a Security Group de AWS
- VNet Peering: equivalente a VPC Peering
- Virtual WAN: equivalente a Transit Gateway
- ExpressRoute: equivalente a Direct Connect

**Tabla comparativa AWS vs Azure:**
- VPC → VNet
- Security Group → NSG
- NAT Gateway → NAT Gateway (mismo nombre)
- Transit Gateway → Virtual WAN Hub
- Direct Connect → ExpressRoute
- Route Table → Route Table (mismo nombre)
- Internet Gateway → no tiene equivalente exacto (implícito en Azure)

### Cap 08 — Multicast

**Unicast vs Broadcast vs Multicast vs Anycast:**
- Unicast: 1 a 1
- Broadcast: 1 a todos (no sale del dominio L2/L3)
- Multicast: 1 a grupo de interesados
- Anycast: 1 al más cercano del grupo (DNS, CDNs)
- Tabla comparativa + casos de uso

**Direcciones multicast IPv4:**
- Rango: 224.0.0.0/4 (Clase D)
- Well-known: 224.0.0.1 (todos los hosts), 224.0.0.2 (todos los routers), 224.0.0.5 (OSPF)
- SSM (Source-Specific Multicast): 232.0.0.0/8

**IGMP (Internet Group Management Protocol):**
- Protocolo entre hosts y router local
- IGMPv3: permite especificar fuentes (source-specific)
- Mensajes: Membership Query (router→hosts), Membership Report (host→router), Leave Group
- IGMP Snooping: cómo el switch optimiza la entrega

**PIM — Protocol Independent Multicast:**
- "Protocol Independent": funciona sobre cualquier protocolo de unicast routing
- PIM-DM (Dense Mode): flood-and-prune, asume todos quieren el tráfico. Raro hoy.
- PIM-SM (Sparse Mode): opt-in, los routers se registran explícitamente
- Rendezvous Point (RP): punto de encuentro entre fuente y receptores
- RPT (Rooted at RP) → SPT (Shortest Path Tree) switchover

**Diagrama TikZ:** flujo PIM-SM desde fuente → RP → receptores → switchover a SPT

**Casos de uso reales:**
- IPTV (Telmex/Totalplay)
- Trading financiero (market data a miles de traders simultáneos)
- Video conferencing multisite
- Software distribution en datacenter

---

## Compilation & Git Workflow

```bash
# Compile Part 2:
cd "D:/Codigo Abierto/RedesDeDatos"
rm -f *.aux *.log *.out *.toc
lualatex --interaction=nonstopmode ApuntesRedes_Parte2.tex

# Check errors:
grep -c "^!" ApuntesRedes_Parte2.log  # debe ser 0

# Commit after each chapter:
git add chapters_parte2/XX_nombre.tex
git commit -m "docs: parte2 cap X - descripción"
git push
```

## Rename Part 1

```bash
git mv ApuntesRedes.tex ApuntesRedes_Parte1.tex
git mv ApuntesRedes.pdf ApuntesRedes_Parte1.pdf  # if tracked
# Update \input paths inside ApuntesRedes_Parte1.tex (none needed, \input uses chapters/ which is unchanged)
git commit -m "chore: renombrar Parte 1 para consistencia con Parte 2"
git push
```
