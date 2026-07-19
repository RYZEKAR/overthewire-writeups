# Nivel 2 → Nivel 3

## Objetivo

Conectarse al nivel 2 de Bandit y leer un archivo con espacios en el nombre para obtener la contraseña del nivel 3.

---

## Conceptos

- **Espacios en nombres de archivo:** En Linux, los nombres de archivo pueden contener espacios, pero la terminal los interpreta como separadores de argumentos.
- **Escapado con comillas:** Rodear un nombre con espacios entre comillas dobles `"..."` o simples `'...'` permite tratarlo como un solo argumento.
- **Ruta `./`:** Combinado con comillas, permite acceder a archivos con nombres complejos.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **ls** — Listar archivos
- **cat** — Leer archivos

---

## Comandos utilizados

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
ls
cat ./"--spaces in this filename--"
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 2 (click para revelar)</summary>

`PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`
</details>

### Paso 2: Listar archivos

```bash
bandit2@bandit:~$ ls
```

**Resultado:**
```
spaces in this filename
```

Un archivo con espacios en el nombre.

### Paso 3: Leer el archivo

Si intentaba `cat spaces in this filename`, Bash lo interpretaría como 4 argumentos separados. Para evitarlo, usé comillas dobles y ruta explícita:

```bash
bandit2@bandit:~$ cat ./"--spaces in this filename--"
```

El `./` fija la ruta al directorio actual, y las comillas dobles agrupan todo el nombre como un solo argumento.

<details>
<summary>🔑 Contraseña obtenida para bandit3 (click para revelar)</summary>

`7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`
</details>

### Paso 4: Cerrar sesión

```bash
bandit2@bandit:~$ exit
```

---

## Resultado

Nivel 2 completado. Se leyó exitosamente un archivo con espacios en el nombre usando comillas dobles para escapar el nombre completo.

---

## Lo que aprendí

- Los nombres de archivo con espacios deben ir entre comillas para que Bash no los divida en argumentos múltiples.
- Se pueden usar comillas dobles `"..."` o simples `'...'`.
- Otra alternativa es escapar cada espacio con una barra invertida: `cat spaces\ in\ this\ filename`.
- La combinación `./` + `"nombre con espacios"` es la forma más clara y segura.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man bash` (sección sobre quoting)
- `man ls`
- `man cat`

---

## Notas

- En escenarios reales, los espacios en nombres de archivo son comunes, especialmente en archivos descargados de Windows o con nombres generados por usuarios.
- Es buena práctica usar Tab para autocompletar: Bash escapa automáticamente los espacios por ti.
