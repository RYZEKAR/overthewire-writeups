# Nivel 4 → Nivel 5

## Objetivo

Conectarse al nivel 4 de Bandit y encontrar el único archivo legible entre varios archivos con formato no humano para obtener la contraseña del nivel 5.

---

## Conceptos

- **Comando `file`:** Determina el tipo real de un archivo (ASCII text, data, PNG, ELF, etc.) leyendo sus bytes mágicos, no su extensión.
- **Glob `./*`:** Expande a todos los archivos en el directorio actual, útil para pasar múltiples archivos como argumentos.
- **Archivos con nombres `-`:** Se leen con `./` para evitar que Bash los interprete como flags.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **file** — Identificar tipo de archivos
- **cat** — Leer archivos

---

## Comandos utilizados

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
file ./*
cat ./-file07
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 4 (click para revelar)</summary>

`xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`
</details>

### Paso 2: Explorar

```bash
bandit4@bandit:~$ ls
```

**Resultado:** `inhere`

```bash
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
```

**Resultado:**
```
-file00  -file01  -file02  -file03  -file04
-file05  -file06  -file07  -file08  -file09
```

Diez archivos, todos con nombres que empiezan con `-`.

### Paso 3: Identificar tipos de archivo

Usé `file` con glob para analizar todos a la vez:

```bash
bandit4@bandit:~/inhere$ file ./*
```

**Resultado:**
```
./-file00: data
./-file01: data
./-file02: OpenPGP Secret Key
./-file03: data
./-file04: data
./-file05: data
./-file06: Non-ISO extended-ASCII text
./-file07: ASCII text
./-file08: data
./-file09: data
```

Solo `-file07` era `ASCII text`. Los demás eran datos binarios.

### Paso 4: Leer el archivo correcto

```bash
bandit4@bandit:~/inhere$ cat ./-file07
```

<details>
<summary>🔑 Contraseña obtenida para bandit5 (click para revelar)</summary>

`6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`
</details>

### Paso 5: Cerrar sesión

```bash
bandit4@bandit:~/inhere$ exit
```

---

## Resultado

Nivel 4 completado. Se usó `file ./*` para identificar entre 10 archivos cuál contenía texto legible, y se leyó con `cat ./-file07`.

---

## Lo que aprendí

- El comando `file` es esencial para identificar tipos de archivos reales, más allá de extensiones o nombres.
- El glob `./*` combinado con `file` permite analizar múltiples archivos rápidamente.
- No hay que asumir que todos los archivos en un directorio son iguales; `file` ayuda a filtrar.
- Los archivos con nombre `-` se leen correctamente anteponiendo `./`.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man file`
- `man ls`
- `man cat`

---

## Notas

- El comando `file` lee los "magic bytes" (primeros bytes del archivo) para identificar el formato.
- `file -i` muestra el MIME type en lugar de la descripción.
- Siempre conviene inspeccionar archivos desconocidos con `file` antes de abrirlos.
