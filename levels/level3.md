# Nivel 3 → Nivel 4

## Objetivo

Conectarse al nivel 3 de Bandit y encontrar un archivo oculto dentro de un directorio para obtener la contraseña del nivel 4.

---

## Conceptos

- **Archivos ocultos en Linux:** Los archivos y directorios cuyo nombre comienza con un punto (`.`) se consideran ocultos.
- **`ls -a`:** El flag `-a` (all) muestra todos los archivos, incluidos los ocultos.
- **`ls -la`:** Combina `-l` (formato largo) con `-a` para ver detalles de todos los archivos.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **cat** — Leer archivos
- **cd** — Cambiar de directorio

---

## Comandos utilizados

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
ls -la
cat ...Hiding-From-You
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 3 (click para revelar)</summary>

`7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`
</details>

### Paso 2: Explorar el directorio home

```bash
bandit3@bandit:~$ ls
```

**Resultado:**
```
inhere
```

Había un directorio llamado `inhere`.

### Paso 3: Entrar al directorio

```bash
bandit3@bandit:~$ cd inhere
```

### Paso 4: Listar archivos (sin ver el oculto)

```bash
bandit3@bandit:~/inhere$ ls
```

**Resultado:** No mostró nada. Solo con `ls` los archivos ocultos no se ven.

### Paso 5: Listar todos los archivos con `-la`

```bash
bandit3@bandit:~/inhere$ ls -la
```

**Resultado:**
```
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You
```

Apareció un archivo oculto: `...Hiding-From-You`.

### Paso 6: Leer el archivo

```bash
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
```

<details>
<summary>🔑 Contraseña obtenida para bandit4 (click para revelar)</summary>

`xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`
</details>

### Paso 7: Cerrar sesión

```bash
bandit3@bandit:~/inhere$ exit
```

---

## Resultado

Nivel 3 completado. Se identificó un directorio `inhere` que contenía un archivo oculto (nombre comenzando con `.`). Se usó `ls -la` para revelarlo y `cat` para leerlo.

---

## Lo que aprendí

- Los archivos que empiezan con `.` son ocultos en Linux y no aparecen con `ls` a secas.
- `ls -a` los muestra; `ls -la` los muestra con detalles (permisos, tamaño, fecha).
- El flag `-l` da formato largo con información detallada.
- Los nombres de archivo pueden comenzar con un punto, y esos archivos se usan comúnmente para configuraciones (`.bashrc`, `.gitignore`, etc.).

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man ls`
- `man cat`
- `man cd`

---

## Notas

- Además de `.` y `..` (directorio actual y padre), cualquier archivo que empiece con `.` se considera oculto.
- `ls -A` muestra casi todos los ocultos excepto `.` y `..`.
