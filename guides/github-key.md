# 🔐 Configuración SSH y Git

## Pasos para configurar SSH y clonar repositorio

### 1. Generar clave SSH
```bash
ssh-keygen -t ed25519 -C "mail@example.com"
```
> Genera una nueva clave SSH usando el algoritmo ed25519 con tu email como comentario.

### 2. Modificar el fichero ~/.ssh/config

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

AlternativamentE:

### 2.1. Iniciar el agente SSH
```bash
eval "$(ssh-agent -s)"
```

### 2.2. Añadir la clave privada al agente
```bash
ssh-add ~/.ssh/id_ed25519
```

### 4. Clonar el repositorio
```bash
git clone git@github.com:estif95/giglon-devops.git
```
---

## 📝 Notas adicionales

- **Importante**: Después del paso 1, debes copiar la clave pública (`~/.ssh/id_ed25519.pub`) y añadirla a tu cuenta de GitHub en **Settings > SSH and GPG keys**.
- Si es la primera vez que te conectas al servidor, confirma la autenticidad del host cuando se te solicite.
- Puedes verificar que la clave se añadió correctamente con: `ssh-add -l`