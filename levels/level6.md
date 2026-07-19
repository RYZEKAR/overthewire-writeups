# Nivel 6 → Nivel 7

## Objetivo

Conectarse al nivel 6 de Bandit y encontrar un archivo en todo el sistema que pertenezca al usuario bandit7 y al grupo bandit6, con un tamaño de exactamente 33 bytes.

---

## Conceptos

- **Búsqueda en todo el sistema:** `find /` busca desde la raíz del sistema de archivos.
- **`-user`:** Filtra por propietario del archivo.
- **`-group`:** Filtra por grupo propietario.
- **Permisos denegados:** Al buscar en `/` como usuario normal, muchos directorios no son accesibles. `find` muestra errores pero continúa.
- **Redirección de errores:** Se puede usar `2>/dev/null` para ocultar los errores y ver solo resultados exitosos.

---

## Herramientas utilizadas

- **SSH** — Conexión remota
- **Bash** — Terminal de Linux
- **find** — Buscar archivos con filtros
- **cat** — Leer archivos

---

## Comandos utilizados

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
ls
find / -user bandit7 -group bandit6 -size 33c
cat /var/lib/dpkg/info/bandit7.password
exit
```

---

## Desarrollo

### Paso 1: Conexión al servidor

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

<details>
<summary>🔑 Contraseña del nivel 6 (click para revelar)</summary>

`pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`
</details>

### Paso 2: Verificar home

```bash
bandit6@bandit:~$ ls
```

No había nada en el directorio home. El archivo está en otra parte del sistema.

### Paso 3: Buscar desde la raíz

Usé `find` desde `/` con los criterios del nivel:

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
```

**Resultado entre los errores:**
```
/var/lib/dpkg/info/bandit7.password
```

El archivo estaba en `/var/lib/dpkg/info/bandit7.password`. Los múltiples errores de "Permission denied" son normales al buscar en todo el sistema sin ser root.

> Para una salida más limpia se puede usar: `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

### Paso 4: Leer el archivo

```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
```

<details>
<summary>🔑 Contraseña obtenida para bandit7 (click para revelar)</summary>

`Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`
</details>

### Paso 5: Cerrar sesión

```bash
bandit6@bandit:~$ exit
```

---

## Resultado

Nivel 6 completado. Se buscó en todo el sistema usando `find /` con los filtros `-user`, `-group` y `-size`, ignorando los errores de permisos, y se encontró el archivo en `/var/lib/dpkg/info/`.

---

## Lo que aprendí

- `find /` busca desde la raíz del sistema, no solo del directorio actual.
- `-user` y `-group` filtran por propietario y grupo del archivo.
- Al buscar en `/`, muchos directorios generan "Permission denied", pero `find` muestra los resultados igual.
- Se puede limpiar la salida redirigiendo errores con `2>/dev/null`.
- Los archivos de contraseñas pueden estar en ubicaciones del sistema como `/var/lib/dpkg/info/`.

---

## Referencias

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- `man find`
- `man cat`

---

## Notas

- La redirección `2>/dev/null` es muy útil para ignorar errores y ver solo lo que importa.
- También se puede usar `-readable` en `find` para filtrar solo archivos legibles por el usuario actual.
