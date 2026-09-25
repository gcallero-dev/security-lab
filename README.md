# Laboratorio Red Team / Blue Team — Guía de configuración segura

Objetivo: practicar ataque (red team) y defensa (blue team) en un entorno **aislado**, usando máquinas vulnerables ya diseñadas para esto, documentar cada ejercicio y publicarlo en GitHub como prueba de capacidad real ante empresas.

No se escribe malware real desde cero. Se usan plataformas educativas con máquinas legales, controladas y pensadas para practicar sin riesgo.

## 1. Aislamiento del entorno (paso obligatorio antes de nada)

1. Instala un virtualizador. En Apple Silicon: **UTM** (gratuito, motor "Virtualización de Apple" — más estable que QEMU en M1/M2/M3 para esto). En Intel: VirtualBox o VMware sirven igual.
2. Para practicar en TryHackMe necesitas que la VM tenga **salida normal a internet** (red compartida/NAT) — te conectas a sus máquinas por OpenVPN, así que aquí NO uses red aislada. El modo "Host-only" aislado se reserva para cuando trabajes offline con VulnHub o software potencialmente peligroso.
3. Antes de cada ejercicio, haz una **snapshot** (instantánea) del estado limpio de la VM si tu virtualizador lo permite. Si algo sale mal, restauras en segundos.
4. Usa una VM Kali Linux (gratuita, oficial, preconfigurada con herramientas de pentesting) como tu "máquina atacante".
5. Para trabajar cómodo (copiar/pegar, texto grande): activa SSH dentro de Kali (`sudo systemctl enable --now ssh`) y conéctate desde la Terminal nativa de tu Mac en vez de la ventana de UTM. Alias configurado: `ssh kali`.

## 2. Plataformas para practicar (máquinas ya hechas, legales)

| Plataforma | Para qué sirve | Nivel |
|---|---|---|
| **TryHackMe** | Salas guiadas paso a paso, explican mientras practicas | Principiante |
| **HackTheBox** | Máquinas más libres, estilo CTF, menos guía | Intermedio |
| **VulnHub** | Máquinas descargables para montar tú mismo en VirtualBox, 100% offline | Intermedio |
| **Blue Team Labs Online** | Ejercicios específicos de defensa (análisis de logs, detección de intrusiones) | Principiante-Intermedio |

Empieza por TryHackMe (rutas "Pre Security" y "Jr Penetration Tester") porque explica el porqué de cada paso, no solo el qué — coincide con la base de "redes + Linux" que ya tienes planeada en el Checkpoint 1.

## 3. Estructura de práctica: Red Team vs Blue Team

- **Red Team (ataque):** en la VM Kali, contra una máquina vulnerable de TryHackMe/HackTheBox/VulnHub. Reconocimiento (Nmap), explotación de la vulnerabilidad, escalada de privilegios.
- **Blue Team (defensa):** analizar qué rastro deja un ataque — logs, tráfico de red (Wireshark), detectar el comportamiento sospechoso, entender cómo se habría bloqueado.

Practicar ambos lados de la misma máquina (primero atacarla, luego analizar qué habría delatado el ataque) es lo que más rápido enseña a pensar como defensor.

## 4. Documentación de cada ejercicio (esto es lo que sube a GitHub)

Por cada máquina resuelta, crea un fichero `writeups/nombre-maquina.md` con esta plantilla:

```markdown
# [Nombre de la máquina] — [Plataforma]

## Objetivo
Qué se pedía conseguir (ej. acceso root, encontrar una flag).

## Reconocimiento
Qué herramientas usaste (Nmap, etc.) y qué encontraste.

## Explotación
Qué vulnerabilidad explotaste y cómo. Comandos usados.

## Qué no funcionó primero
Los intentos fallidos también cuentan — demuestran cómo piensas, no solo el resultado.

## Resultado
Cómo conseguiste el objetivo final.

## Análisis defensivo (Blue Team)
Si tuvieras que defender este sistema: ¿qué log habría delatado el ataque? ¿qué configuración lo habría evitado?

## Qué aprendiste
2-3 líneas de la lección real, no solo "aprendí X herramienta".
```

Esto es exactamente lo que el vídeo que analizamos identificaba como la diferencia entre quien consigue trabajo y quien no: no basta con resolver la máquina, hay que documentarlo de forma que una empresa vea cómo piensas.

## 5. Repositorio de GitHub

Crea un repo separado (no dentro de este proyecto de Flipzea) llamado algo como `ciberseguridad-writeups` o `security-lab`, con esta estructura:

```
security-lab/
├── README.md          (resumen de tu progreso, qué plataformas usas)
├── writeups/
│   ├── tryhackme-nombre1.md
│   ├── htb-nombre2.md
│   └── vulnhub-nombre3.md
└── notas/
    └── redes-linux-fundamentos.md   (tus apuntes del Checkpoint 1)
```

Mínimo 3 máquinas resueltas y documentadas antes de pasar a certificación — es la prueba que marcaba el Checkpoint 2 del plan que ya vimos.

## Progreso (actualizado 26/09/2026)

- [x] UTM instalado, VM "Kali Linux" creada (motor Apple Virtualization, HiDPI activado, 4GB RAM/4 núcleos/64GB disco)
- [x] Kali instalado y actualizado (`apt update && full-upgrade`)
- [x] Acceso cómodo por SSH configurado (`ssh kali` desde Terminal de Mac — copiar/pegar nativo, sin depender de UTM)
- [x] Carpeta compartida Mac↔Kali montada en `/mnt/share` (para pasar archivos largos sin usar el portapapeles gráfico)
- [x] Cuenta creada en TryHackMe
- [x] Ruta "Pre Security" / "Ciberseguridad 101" empezada (14 secciones: redes, Linux, Windows/AD, criptografía, explotación básica, web hacking, seguridad defensiva, SIEM/IDS, carreras)
- [ ] Terminar las 14 secciones de la ruta, sala a sala
- [ ] Primera máquina resuelta y documentada con la plantilla de arriba (ver sección 4)
- [ ] 3 máquinas documentadas → entonces sí, certificación **SEC0 (Pre Security Certificate)**

## Próximo paso
Seguir avanzando sala a sala por la ruta "Pre Security" en TryHackMe (https://tryhackme.com/module/pre-security-introduction). El primer writeup lo documentamos juntos cuando termines tu primera sala práctica de verdad (no solo teoría).
