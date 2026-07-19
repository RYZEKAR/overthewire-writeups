# Nivel 1 → Nivel 2

## Objetivo

Conectarse al nivel 1 de Bandit y leer el archivo con la contraseña para acceder al siguiente nivel (bandit2).

---

## Conceptos

- **Caracteres especiales en Bash:** El guión `-` es un carácter especial en la terminal. Muchos comandos lo interpretan como "entrada estándar" (stdin) o como indicador de opciones/flags.
- **Ruta relativa con `./`:** Anteponer `./` a un nombre de archivo fuerza a Bash a tratarlo como una ruta literal al archivo, evitando que lo interprete como un flag.
- **Redirección y argumentos:** Entender cómo los comandos procesan sus argumentos es clave para resolver este tipo de desafíos.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **cat** — Leer archivos

---

## Comandos utilizados

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
ls
cat ./-
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

Me conecté al nivel 1 usando SSH:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 1 (click para revelar)</summary>

`ZjLK...` <!-- El usuario reemplazará con la real -->
</details>

> La contraseña de bandit1 se obtuvo al completar el nivel 0.

### Paso 2: Listar archivos

Una vez dentro, listé el contenido del directorio home:

```bash
bandit1@bandit:~$ ls
```

**Resultado:**
```
-
```

Solo había un archivo, pero con un nombre muy peculiar: un simple guión (`-`).

### Paso 3: Intentar leer el archivo (el truco)

Intenté leerlo de forma directa:

```bash
bandit1@bandit:~$ cat -
```

Pero el comando se quedó esperando entrada del teclado porque Bash interpreta el `-` como "leer desde stdin" (entrada estándar). Tuve que interrumpirlo con `Ctrl + C`.

**El problema:** El guión `-` es un carácter reservado en Bash. Muchos comandos como `cat`, `cd`, `echo`, etc., lo interpretan como un argumento especial, no como un nombre de archivo.

**La solución:** Usar una ruta explícita con `./` (directorio actual):

```bash
bandit1@bandit:~$ cat ./-
```

**Resultado:** El comando mostró la contraseña para el nivel 2:

<details>
<summary>🔑 Contraseña obtenida para bandit2 (click para revelar)</summary>

`PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`
</details>

### Paso 4: Cerrar sesión

```bash
bandit1@bandit:~$ exit
```

---

## Resultado

Nivel 1 completado. Se identificó que el archivo con la contraseña tenía el nombre `-`, un carácter especial en Bash, y se utilizó `cat ./-` para leerlo correctamente evitando la interpretación especial del guión.

---

## Lo que aprendí

- El guión `-` no es un nombre de archivo normal en Bash; muchos comandos lo interpretan como un argumento especial (stdin, flag, etc.).
- Para leer archivos con nombres problemáticos, se puede anteponer `./` para desambiguar: `cat ./-`.
- Otras alternativas incluyen usar la ruta absoluta `cat /home/bandit1/-` o escapar el nombre con `cat -- -`.
- Este tipo de trucos es común en desafíos de seguridad y wargames.
- A veces la dificultad no está en el contenido, sino en cómo acceder a él.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- [Bash Special Characters](https://www.gnu.org/software/bash/manual/html_node/Special-Parameters.html)
- `man bash` (sección sobre caracteres especiales)
- `man cat`

---

## Notas

- El archivo con nombre `-` es un ejemplo clásico de cómo los nombres de archivo pueden colisionar con la sintaxis de comandos.
- También se puede usar el flag `--` para indicar "fin de opciones": `cat -- -`.
