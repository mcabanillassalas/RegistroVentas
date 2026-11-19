# RegistroVentas

Proyecto educativo de registro de ventas en Solana. Este repositorio reúne los dos proyectos originales del bootcamp:

- **Backend:** programa on-chain en Rust y Anchor. Define las cuentas Registro, Cliente y Venta, sus PDAs e instrucciones.
- **Frontend:** aplicación React, TypeScript y Vite para consultar las cuentas y enviar operaciones con una wallet.

El backend no es un servidor HTTP: una vez desplegado, sus instrucciones se ejecutan en Solana. El frontend se ejecuta en el navegador y se conecta al programa mediante un RPC.

## Estructura

```text
RegistroVentas/
├── backend/   # Programa Anchor y cliente de Solana Playground
├── frontend/  # Aplicación React/Vite, IDL y cliente TypeScript
├── .gitignore
└── README.md
```

Consulta las instrucciones específicas de cada parte:

- [Backend: importación y uso con Solana Playground](./backend/README.md)
- [Frontend: instalación, desarrollo y configuración del IDL](./frontend/README.md)
- [Guía de pruebas del frontend en Devnet](./frontend/docs/PRUEBAS-MANUALES.md)

## Flujo general

1. Compila y despliega el programa backend en **Devnet** desde Solana Playground.
2. Exporta el IDL del mismo programa desplegado.
3. Importa ese IDL en el frontend y genera el cliente TypeScript.
4. Ejecuta el frontend y realiza operaciones con una wallet configurada en Devnet.

El frontend incluye inicialmente un IDL de referencia; las escrituras permanecen bloqueadas hasta importar el IDL del despliegue que se va a utilizar. El Program ID, el IDL y el cliente generado deben corresponder al mismo programa y versión.

Para desarrollo local del frontend, abre PowerShell:

```powershell
cd D:\DevWayLearn\proyecto-final\RegistroVentas\frontend
npm ci
npm run verificar
npm run dev
```

Abre `http://localhost:5173`. La configuración predeterminada usa el RPC público de Devnet. Consulta [frontend/README.md](./frontend/README.md) para importar el IDL y los detalles de configuración.

El backend original está preparado para Solana Playground. Los archivos `backend/src/lib.rs` y `backend/tests/anchor.test.ts` son material del programa de clase; el test incluido es una plantilla que invoca `initialize`, instrucción que no pertenece a RegistroVentas. Consulta el README del backend antes de usar las opciones de prueba de Playground.

El README del backend importa el repositorio original independiente del programa. En este monorepo, el código está dentro de `backend/`; no asumas que Solana Playground podrá importar el repositorio combinado desde su raíz como si fuera el repositorio standalone. Para desplegar, sigue el enlace del README del backend o publica/importa el backend como repositorio independiente. El monorepo combinado puede seguir siendo el repositorio de entrega.

## Entorno requerido

- Node.js `>=22.12.0 <25` y npm para el frontend.
- Wallet de navegador compatible con Solana y SOL de prueba en Devnet para enviar transacciones.
- Solana Playground y una wallet de prueba en Devnet para compilar y desplegar el programa.

No es necesario dejar un validador local de WSL ejecutándose para utilizar el despliegue de Devnet.

## Seguridad y alcance

- No subas frases de recuperación, claves privadas, archivos de wallet ni keypairs de programa.
- No subas archivos `.env.local` ni otros archivos con configuración privada. El `.env.example` del frontend solo muestra la variable pública de RPC.
- No subas `node_modules`, `dist`, `target`, ledgers de validadores locales ni archivos temporales de desarrollo; están excluidos por `.gitignore`.
- Esta es una base educativa para Devnet, no una aplicación auditada para producción.

## Publicar este monorepo en GitHub

1. En GitHub, crea un repositorio vacío para el proyecto. Para evitar conflictos al primer `push`, no inicialices el remoto con README, `.gitignore` ni licencia.
2. Desde PowerShell, ejecuta en la raíz `D:\DevWayLearn\proyecto-final\RegistroVentas`:

   ```powershell
   git init -b main
   git add README.md .gitignore backend frontend
   git status --short
   git diff --cached --stat
   ```

3. Revisa el estado y confirma que no se prepararon claves, wallets, archivos `.env.local`, `node_modules`, `dist` ni `target`. Si todo está correcto:

   ```powershell
   git commit -m "Initial RegistroVentas project"
   git remote add origin https://github.com/TU_USUARIO/TU_REPOSITORIO.git
   git push -u origin main
   ```

   Reemplaza la URL por la del repositorio vacío que creaste. GitHub autenticará el `push` mediante el navegador o Git Credential Manager; no pongas tokens en el comando ni en archivos del proyecto.

4. Abre la página del repositorio en GitHub y comprueba que aparecen `backend/`, `frontend/`, el README y los archivos de configuración versionados.

Si Git informa que `user.name` o `user.email` no están configurados, configúralos en tu equipo antes del `commit`. No es necesario añadir ni publicar carpetas de `zMax` para subir este proyecto.
