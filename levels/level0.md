# Nivel 0 → Nivel 1

## Objetivo

Conectarse al servidor de OverTheWire Bandit mediante SSH y encontrar la contraseña para acceder al siguiente nivel (bandit1).

---

## Conceptos

- **SSH (Secure Shell):** Protocolo que permite conectarse de forma segura a un servidor remoto.
- **Puerto:** Número que identifica un servicio específico en un servidor. OverTheWire usa el puerto **2220** en lugar del puerto SSH estándar (22).
- **Autenticación por contraseña:** Método de inicio de sesión donde se ingresa usuario y contraseña.

---

## Herramientas utilizadas

- **SSH** — Cliente de conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos y directorios
- **cat** — Leer contenido de archivos
- **file** — Determinar el tipo de un archivo

---

## Comandos utilizados

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
file readme
cat readme
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

Desde mi terminal, ejecuté el comando para conectarme al servidor de Bandit:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

- `ssh`: comando para iniciar una conexión SSH.
- `bandit0`: usuario del nivel 0.
- `bandit.labs.overthewire.org`: dominio del servidor.
- `-p 2220`: especifica el puerto 2220 (el puerto SSH por defecto es 22, pero Bandit usa este alternativo).

Al ejecutarlo, el sistema solicita la contraseña del nivel 0.

<details>
<summary>🔑 Contraseña del nivel 0 (click para revelar)</summary>

`bandit0`
</details>

> **Nota:** La contraseña se ingresa escribiéndola (no se ve mientras tecleas por seguridad). Luego presionas Enter.

### Paso 2: Explorar el directorio home

Una vez conectado, listé los archivos en el directorio home para ver qué había:

```bash
bandit0@bandit:~$ ls
```

**Resultado:**
```
readme
```

Había un único archivo llamado `readme`.

### Paso 3: Verificar el tipo de archivo

Antes de abrirlo, verifiqué qué tipo de archivo era por seguridad:

```bash
bandit0@bandit:~$ file readme
```

**Resultado:**
```
readme: ASCII text
```

Era un archivo de texto ASCII, seguro para leerlo directamente.

### Paso 4: Leer el archivo

Usé `cat` para mostrar el contenido del archivo:

```bash
bandit0@bandit:~$ cat readme
```

**Resultado:** El archivo contenía la contraseña para acceder al siguiente nivel (bandit1).

### Paso 5: Cerrar sesión

Finalmente, salí del servidor:

```bash
bandit0@bandit:~$ exit
```

---

## Resultado

Nivel 0 completado correctamente. Se estableció conexión SSH exitosa, se exploró el directorio home, se identificó y leyó el archivo `readme`, y se obtuvo la contraseña para el nivel 1.

<details>
<summary>🔑 Contraseña obtenida para bandit1 (click para revelar)</summary>

`6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` <!-- Contraseña real omitida para spoilers parciales, el usuario la reemplazará -->
</details>

---

## Lo que aprendí

- SSH permite conectarse a servidores remotos de forma segura usando el puerto indicado con `-p`.
- El comando `ls` lista los archivos del directorio actual.
- El comando `file` identifica el tipo de archivo.
- El comando `cat` muestra el contenido de archivos de texto.
- Las contraseñas en SSH se ingresan enmascaradas (no se ven al teclear).
- Incluso en desafíos simples, verificar el tipo de archivo con `file` es una buena práctica de seguridad.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man ssh`
- `man ls`
- `man cat`
- `man file`

---

## Notas

- OverTheWire Bandit es un wargame ideal para principiantes que quieren aprender Linux y Bash.
- No uses la contraseña de bandit0 para nada fuera de este entorno educativo.
- Las contraseñas de OverTheWire cambian periódicamente, pueden diferir de las de otras guías.
