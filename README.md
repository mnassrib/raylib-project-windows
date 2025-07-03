# 🎮 Raylib Project (Windows)

Ce projet montre comment structurer un projet en langage C avec la bibliothèque [Raylib](https://www.raylib.com/) sous Windows, en utilisant **CMake** et **MinGW-w64**. Il inclut également un workflow GitHub Actions pour la compilation automatique sous Windows.

---

## 📁 Structure du projet

```

raylib-project-windows/
├── CMakeLists.txt           # Configuration du projet (CMake)
├── src/                     # Fichiers source (.c)
│   ├── main.c
│   ├── player.c
│   └── utils.c
├── include/                 # Fichiers d’en-tête (.h)
│   ├── player.h
│   └── utils.h
├── build/                   # Dossier de compilation (généré)
└── .github/
    └── workflows/
        └── ci-windows.yml   # GitHub Actions (Windows)

````

---

## ⚙️ Compilation sous Windows

### 📌 Prérequis

- [CMake](https://cmake.org/download/) 
- [MinGW-w64](https://www.mingw-w64.org/)
- [Chocolatey](https://chocolatey.org/) (recommandé pour l’installation automatisée)
- Raylib compilée localement dans `C:/raylib`

> 💡 Raylib ne s’installe pas via `choco` : vous devez la **télécharger manuellement** ou utiliser le [build précompilé ici](https://github.com/raysan5/raylib/releases)

---

### 🧰 Étapes de configuration

1. **Installer Chocolatey (si ce n’est pas déjà fait)**  
   PowerShell (en mode administrateur) :
   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force
   iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
   ```

2. **Installer MinGW et CMake**

   ```powershell
   choco install mingw -y
   choco install cmake -y --installargs 'ADD_CMAKE_TO_PATH=System'
   ```

3. **Compiler et installer Raylib**

   ```cmd
   git clone https://github.com/raysan5/raylib.git
   cd raylib
   mkdir build && cd build
   cmake -G "MinGW Makefiles" -DBUILD_EXAMPLES=OFF ..
   mingw32-make
   cmake --install . --prefix "C:/raylib"
   ```

---

## 🚀 Compilation du projet

```cmd
git clone https://github.com/votre-utilisateur/raylib-project-windows.git
cd raylib-project-windows
mkdir build && cd build
cmake -G "MinGW Makefiles" -DCMAKE_PREFIX_PATH="C:/raylib" ..
mingw32-make
.\raylib_project.exe
```

---

## ✅ Intégration Continue

Ce projet est automatiquement compilé sous Windows via GitHub Actions à chaque `push` :

![CI Status](https://github.com/mnassrib/raylib-project-windows/actions/workflows/ci-windows.yml/badge.svg)

---

## 📄 Ressources utiles

* [Raylib — Site officiel](https://www.raylib.com/)
* [MinGW-w64](https://www.mingw-w64.org/)
* [CMake Documentation](https://cmake.org/documentation/)

---

## 📜 Licence

Ce projet est librement utilisable à des fins pédagogiques et de formation.