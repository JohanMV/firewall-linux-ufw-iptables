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
      <td>Verificar el estado inicial de red y firewall</td>
      <td>ifconfig, ss -tulnp, ufw status, iptables -L</td>
      <td>Confirmar que la interfaz de red está activa, detectar servicios en escucha y validar que no existen reglas previas activas</td>
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

---

<h3>1️⃣ Verificar el estado inicial de red y firewall</h3>

---

En este primer paso nos aseguramos que el entorno esté limpio y funcional antes de aplicar reglas de firewall. 

<img src="./Evidencias/Figura_1 - Verificar el estado inicial de red y firewall.png" alt="Verificar el estado inicial de red y firewall" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> 

<br>
De esta forma garantizamos que cualquier bloqueo posterior sea atribuible únicamente a las reglas que aplicaremos y no a configuraciones residuales.

<br> 

<pre>La máquina tenga una IP válida (verificado con ifconfig)</pre>

<pre> No existan servicios inesperados abiertos (ss -tulnp)</pre>

<pre>El firewall UFW esté inactivo (ufw status)</pre>

<pre>No haya reglas previas en IPTables (iptables -L)</pre>



<h3>2️⃣ Aplicar políticas predeterminadas y permitir servicios esenciales</h3>

---

Estableceremos las reglas mínimas para que la máquina solo permita conexiones salientes y bloquee cualquier intento de conexión entrante no autorizado. Esto es una medida base recomendada por los CIS Benchmarks para servidores.

🎯 El objetivo será: 

* Bloquear todo el tráfico entrante por defecto (deny incoming)

* Permitir todo el tráfico saliente (allow outgoing)

* Habilitar el acceso por SSH (puerto 22) para administración remota (opcional)

* Activar el firewall UFW y verificar el estado

<img src="./Evidencias/Figura_2 - Aplicar politicas y activar el Firewall.png" alt="Aplicar politicas y activar el Firewall" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> <br> 

Resultado esperado:

    🔒 Todo tráfico entrante no autorizado es bloqueado por defecto.

    ✅ El tráfico saliente (como actualizaciones del sistema) se mantiene habilitado.

    🔓 El puerto 22/tcp queda accesible para conexiones SSH (seguridad remota).

    📊 El estado del firewall se puede verificar con ufw status verbose.

🛡️ En este paso sentamos la base de una política de mínimo privilegio, recomendada por los **CIS Brenchmarks (Control 9.1)**.

<h3>3️⃣ Crear reglas personalizadas para proteger el sistema</h3>

---

Ahora fortaleceremos la seguridad más allá de las políticas generales de UFW, aplicando reglas directas en IPTables para controlar con precisión el tráfico basado en protocolos, puertos, y direcciones IP.

🔸 3.1 Establecer políticas predeterminadas

    sudo iptables -P INPUT DROP
    sudo iptables -P FORWARD DROP
    sudo iptables -P OUTPUT ACCEPT

🔸 3.2 Permitir tráfico legítimo y conexiones establecidas

    sudo iptables -A INPUT -i lo -j ACCEPT
    sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT


<img src="./Evidencias/Figura_3 - Reglas iptables 1.png" alt=" Reglas iptables" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> 
<br> 

Primero implementamos un enfoque "default deny" y luego evita bloqueos innecesarios y mantiene la funcionalidad normal del sistema sin exponer puertos.

🔸 3.3 Definir reglas explícitas de filtrado

    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT       # Permitir SSH
    sudo iptables -A INPUT -p tcp --dport 23 -j DROP         # Bloquear Telnet
    sudo iptables -A INPUT -s 203.0.113.45 -j DROP           # Bloquear IP específica

<img src="./Evidencias/Firewall_4 - Reglas iptables 2.png" alt="Reglas iptables 2" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> <br> 

Estas reglas personalizadas permiten construir una política de defensa efectiva, basada en el principio de mínimo privilegio.

<h3>4️⃣ Simular escaneos y validar bloqueos </h3>

---

En esta etapa realizamos pruebas de escaneo contra el Firewall configurado con reglas iptables, desde un host externo (máquina física con Windows) utilizando Zenmap (Nmap GUI).

El objetivo fue validar que los servicios no autorizados (puertos no permitidos explícitamente) estén correctamente bloqueados por el firewall.

    nmap -sS -p- 192.168.0.106
    nmap -sV -p22,23,80 192.168.0.106


🔐 Resultado esperado

    Puerto 22 (SSH): Permitido

    Puerto 23 (Telnet): Bloqueado

    Puerto 80 (HTTP): Bloqueado

    Todos los demás puertos: Bloqueados

<img src="./Evidencias/Figura_5 - Ataque Nmap Windows 1.png" alt="Ataque Nmap Windows 1" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> <br> 

<img src="./Evidencias/Figura_6 - Ataque Nmap Windows 2.png" alt="Ataque Nmap Windows 2" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> <br> 

Donde <code>192.168.0.106</code> corresponde a la dirección IP de la máquina con iptables activo (Kali Linux en VirtualBox).

✅ Resultados

* El escaneo con -p- (todos los puertos) no detectó ningún puerto abierto, lo que demuestra que las políticas DROP en iptables están funcionando correctamente.

* El escaneo dirigido a puertos 22, 23 y 80 solo detectó el puerto 22 como abierto, cumpliendo con la regla de permitir SSH y bloquear Telnet y HTTP.

* Se demostró resistencia a técnicas básicas de reconocimiento pasivo y activo.

<h3>5️⃣ Revisar registros del sistema y ajustar reglas si es necesario</h3>

---

En este paso se valida que los eventos sospechosos (intentos de conexión, escaneos, paquetes ICMP, etc.) estén siendo registrados por el sistema y el firewall. Esta fase es clave para detectar actividad no autorizada y afinar las reglas establecidas previamente.

Se activó el registro del firewall con:

```bash
sudo ufw logging on
```

Y se visualizaron eventos bloqueados con:
```
sudo dmesg | grep "IN="
```

<img src="./Evidencias/Figura_7 - UFW.png" alt="UFW" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;"/> <br> 


<h4>📊 Validación visual con Gufw</h4> 

Para complementar la revisión, se utilizó Gufw, la interfaz gráfica de UFW, permitiendo visualizar:

  * Las reglas permitidas (puerto 22/tcp habilitado)

  * Reportes de actividad de red

  * Historial de activación del firewall

  <img src="./Evidencias/Figura_8 - UFW 1.png" alt="UFW 1" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;" />
<br>

<img src="./Evidencias/Figura_9 - UFW 2.png" alt="UFW 2" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;" />
<br>

<img src="./Evidencias/Figura_10 - UFW 3.png" alt="UFW 3" style="width: 100%; height: auto; border: 1px solid #444; border-radius: 8px;" />
<br>