# ✅ Lista de Tarefas

Aplicativo mobile de lista de tarefas feito com **React Native + Expo**, com banco de dados local (SQLite), perfil de usuário com foto tirada pela câmera e autenticação com **Firebase** (email/senha e Google).

## 🛠 Tecnologias

- Expo SDK 57 + React Native 0.86 + TypeScript
- Expo Router (rotas baseadas em arquivos)
- NativeWind (Tailwind CSS no React Native)
- expo-sqlite (banco local)
- expo-camera + expo-file-system (foto de perfil)
- Firebase Authentication (email/senha e Google)
- expo-auth-session (login com Google)

## ✨ Funcionalidades

- Criar, editar, concluir e excluir tarefas
- Filtrar tarefas (todas, pendentes, concluídas)
- Perfil do usuário com foto tirada pela câmera
- Cadastro e login com email e senha
- Login com Google
- Rotas protegidas: sem login, o app mostra apenas as telas de login e cadastro
- Sessão persistente: o usuário continua logado ao reabrir o app

## 📁 Estrutura do projeto

```
app/
  _layout.tsx        Layout raiz + proteção de rotas
  index.tsx          Lista de tarefas
  form.tsx           Criar/editar tarefa
  profile.tsx        Perfil com foto
  login.tsx          Tela de login
  register.tsx       Tela de cadastro
src/
  components/        TaskItem, FilterBar, EmptyState, CameraCapture
  contexts/          AuthContext
  database/          SQLite: conexão e repositórios
  hooks/             useTasks, useProfile, useAuth
  services/          firebaseConfig
  types/             Tipos TypeScript
.env.example         Modelo das variáveis de ambiente
```

## 🏗 Arquitetura

- **Telas** (`app/`) só cuidam da interface.
- **Hooks** (`src/hooks/`) concentram a lógica e o estado.
- **Repositórios** (`src/database/`) concentram o acesso ao SQLite.
- **AuthContext** compartilha o usuário logado com todo o app, e o `_layout.tsx` redireciona para `/login` quando não há sessão.

## 🗄 Banco de dados

SQLite local, com as tabelas `tasks` (tarefas) e `profile` (nome e foto do perfil). As tabelas são criadas automaticamente na primeira execução.

## 🚀 Como rodar

Pré-requisitos: Node.js 22.13 ou superior, Git e o app **Expo Go (versão SDK 57)** no celular.

```bash
git clone <URL-DO-REPOSITORIO>
cd meu-lista-tarefas
npm install --legacy-peer-deps
cp .env.example .env
```

Preencha o arquivo `.env` com os dados do seu projeto Firebase (veja abaixo) e inicie:

```bash
npx expo start --clear
```

Escaneie o QR Code com o Expo Go. Se o celular não conectar, use `npx expo start --tunnel`.

## 🔥 Configuração do Firebase

1. Acesse https://console.firebase.google.com e crie um projeto.
2. Em **Visão geral do projeto**, clique no ícone **Web (`</>`)** e registre um app. Copie os valores do `firebaseConfig`.
3. Em **Authentication > Sign-in method**, ative **Email/senha** e **Google**.
4. No provedor Google, em **Configuração do SDK da Web**, copie o **ID do cliente da Web**.
5. Coloque tudo no `.env`:

```
EXPO_PUBLIC_FIREBASE_API_KEY=...
EXPO_PUBLIC_FIREBASE_AUTH_DOMAIN=...
EXPO_PUBLIC_FIREBASE_PROJECT_ID=...
EXPO_PUBLIC_FIREBASE_STORAGE_BUCKET=...
EXPO_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=...
EXPO_PUBLIC_FIREBASE_APP_ID=...
EXPO_PUBLIC_GOOGLE_WEB_CLIENT_ID=...
```

Sem aspas e sem espaços. O arquivo `.env` está no `.gitignore` e **nunca** deve ser enviado ao GitHub.

## 📚 Etapas do desenvolvimento

- Etapas 1 a 11: lista de tarefas com SQLite, filtros e navegação.
- Etapas 12 a 19: perfil do usuário e foto pela câmera.
- Etapas 20 a 30: autenticação com Firebase (email/senha e Google), contexto de autenticação e rotas protegidas.

## 🧯 Solução de problemas

- **Expo Go diz que o projeto é incompatível:** instale o Expo Go para o SDK 57 (https://expo.dev/go).
- **Erro de Firebase / variáveis undefined:** confira o `.env` e reinicie com `npx expo start --clear`.
- **`auth/invalid-credential`:** email ou senha incorretos.
- **`auth/operation-not-allowed`:** ative Email/senha em Authentication > Sign-in method.
- **Erro no `npm install`:** use `npm install --legacy-peer-deps`.
- **Login com Google falha no Expo Go:** o login por email e senha funciona normalmente; o Google pode exigir um build de desenvolvimento.
