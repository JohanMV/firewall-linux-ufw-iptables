## 🌐 Español
# 🔐 Firewall Personalizado con UFW e IPTables

Este proyecto simula la implementación y configuración de un firewall personalizado en un entorno Linux, utilizando UFW como interfaz de gestión y reglas avanzadas mediante IPTables. El objetivo es mejorar la postura defensiva de una máquina servidor, controlar el tráfico entrante y saliente, y proteger servicios críticos frente a ataques internos.

## 🧰 Herramientas utilizadas
- Ubuntu Server
- UFW (Uncomplicated Firewall)
- IPTables
- Nmap
- hping3 / netcat

## 🔍 Metodología aplicada
1. Verificación de conectividad entre interfaces
2. Aplicación de políticas predeterminadas de UFW (deny incoming, allow outgoing)
3. Definición de puertos y servicios esenciales permitidos
4. Integración de reglas avanzadas de IPTables para refuerzo (DROP, REJECT, filtrado por protocolo/IP)
5. Simulación de escaneos y ataques para validación
6. Revisión de logs y documentación

## 📄 Informe final
El informe documenta el comportamiento del firewall bajo diferentes condiciones, evidencia el bloqueo de escaneos, ataques ICMP y puertos no autorizados, y ofrece recomendaciones de mejora alineadas a los CIS Benchmarks (nivel 1). Se incluye comparación entre enfoques UFW y reglas manuales con IPTables.

---

<details>
<summary><h2>🌍 English</h2></summary>

# 🔐 Custom Firewall with UFW and IPTables

This project simulates the implementation and configuration of a custom firewall in a Linux environment, using UFW as a management interface and advanced rules with IPTables. The objective is to improve the defensive posture of a server machine, control incoming and outgoing traffic, and protect critical services against internal attacks.

## 🧰 Tools Used
- Ubuntu Server
- UFW (Uncomplicated Firewall)
- IPTables
- Nmap
- hping3 / netcat

## 🔍 Applied Methodology
1. Connectivity check between interfaces
2. Application of UFW default policies (deny incoming, allow outgoing)
3. Definition of essential ports and allowed services
4. Integration of advanced IPTables rules for hardening (DROP, REJECT, protocol/IP filtering)
5. Attack and scan simulation for validation
6. Log review and documentation

## 📄 Final Report
The report documents the firewall behavior under various conditions, evidences the blocking of scans, ICMP attacks, and unauthorized ports, and offers improvement recommendations aligned with CIS Benchmarks (Level 1). A comparison between UFW and manual IPTables rules is also included.

</details>

<h2>🧭 Flujo Técnico del Proyecto</h2>

<table>
  <thead>
    <tr>
      <th>Paso</th>
      <th>Acción</th>
      <th>Herramienta</th>
      <th>Resultado esperado</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1️⃣</td>
      <td>Verificar conectividad de red</td>
      <td>ping, ifconfig, nmap</td>
      <td>Confirmar que la máquina está activa y accesible</td>
    </tr>
    <tr>
      <td>2️⃣</td>
      <td>Aplicar políticas predeterminadas y permitir servicios esenciales</td>
      <td>UFW</td>
      <td>Solo puertos específicos accesibles (ej. 22/SSH)</td>
    </tr>
    <tr>
      <td>3️⃣</td>
      <td>Crear reglas personalizadas para proteger el sistema</td>
      <td>IPTables</td>
      <td>Bloqueo de puertos, protocolos o IPs sospechosas</td>
    </tr>
    <tr>
      <td>4️⃣</td>
      <td>Simular escaneos y ataques</td>
      <td>nmap, hping3, netcat</td>
      <td>Comprobar que el firewall bloquea intentos no autorizados</td>
    </tr>
    <tr>
      <td>5️⃣</td>
      <td>Revisar registros y ajustar reglas</td>
      <td>UFW logging, dmesg</td>
      <td>Validar que los eventos sospechosos sean registrados</td>
    </tr>
    <tr>
      <td>6️⃣</td>
      <td>Documentar configuraciones y recomendaciones</td>
      <td>Markdown (README.md)</td>
      <td>Informe estructurado con reglas, pruebas y medidas alineadas a CIS</td>
    </tr>
  </tbody>
</table>
