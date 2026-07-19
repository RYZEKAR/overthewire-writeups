# Nivel 10 → Nivel 11

## Objetivo

Conectarse al nivel 10 de Bandit y decodificar un archivo codificado en base64 para obtener la contraseña.

---

## Conceptos

- **Base64:** Esquema de codificación que convierte datos binarios a texto ASCII. Común en transferencias de datos, emails y APIs.
- **Comando `base64`:** Decodifica (o codifica) datos en formato base64.
- **`base64 -d`:** El flag `-d` (decode) decodifica el contenido.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **file** — Identificar tipo de archivo
- **base64** — Decodificar base64

---

## Comandos utilizados

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
ls
file data.txt
base64 -d data.txt
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 10 (click para revelar)</summary>

`B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`
</details>

### Paso 2: Explorar

```bash
bandit10@bandit:~$ ls
```

**Resultado:** `data.txt`

```bash
bandit10@bandit:~$ file data.txt
```

**Resultado:** `data.txt: ASCII text`

### Paso 3: Leer y decodificar

```bash
bandit10@bandit:~$ cat data.txt
```

Mostró una cadena larga con caracteres alfanuméricos y signos `=` al final, típico de base64.

```bash
bandit10@bandit:~$ base64 -d data.txt
```

**Resultado:**
```
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

<details>
<summary>🔑 Contraseña obtenida para bandit11 (click para revelar)</summary>

`pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro`
</details>

### Paso 4: Cerrar sesión

```bash
bandit10@bandit:~$ exit
```

---

## Resultado

Nivel 10 completado. Se decodificó un archivo en base64 usando `base64 -d` para revelar la contraseña.

---

## Lo que aprendí

- Base64 es una codificación, no cifrado. Se usa para representar datos binarios como texto.
- `base64 -d` decodifica; `base64` sin flags codifica.
- También funciona con pipeline: `cat data.txt | base64 -d`.
- El prefijo `The password is` en la salida decodificada indica que el contenido completo estaba codificado.
- Base64 se reconoce fácilmente por los caracteres `A-Za-z0-9+/` y el padding con `=`.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man base64`
- `man file`

---

## Notas

- Base64 es una codificación, no un cifrado. No proporciona seguridad, solo transformación de formato.
- Otros formatos comunes: base32, base16 (hexadecimal).
