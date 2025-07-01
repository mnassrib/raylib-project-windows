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
        └── ci-windows.yml     # GitHub Actions (Windows)

````

---

## ⚙️ Compilation sous Windows

### 📌 Prérequis

- [MinGW-w64](https://www.mingw-w64.org/)
- [CMake](https://cmake.org/)
- Raylib précompilée pour Windows (ZIP)
- VSCode (optionnel mais recommandé)

> 💡 Raylib ne s’installe pas via `choco` : vous devez la **télécharger manuellement** ou utiliser le [build précompilé ici](https://github.com/raysan5/raylib/releases)

---

### 🧱 Étapes

```bash
# 1. Télécharger Raylib pour MinGW depuis :
#    https://github.com/raysan5/raylib/releases

# 2. Extraire l’archive, par exemple dans :
#    C:\raylib

# 3. Vérifier que vous avez :
#    C:\raylib\include
#    C:\raylib\lib\libraylib.a
#    C:\raylib\cmake\raylib-config.cmake

# 4. Cloner ce dépôt
git clone https://github.com/mnassrib/raylib-project-windows.git
cd raylib-project

# 5. Créer un dossier de compilation
mkdir build
cd build

# 6. Configurer avec CMake
cmake .. -G "MinGW Makefiles" -DCMAKE_PREFIX_PATH="C:/raylib"

# 7. Compiler
mingw32-make

# 8. Lancer l’exécutable
./raylib_project.exe
```

---

## ✅ Intégration Continue

Ce projet est automatiquement compilé sous Windows via GitHub Actions à chaque `push` :

![CI Status](https://github.com/mnassrib/raylib-project-windows/actions/workflows/ci-windows.yml/badge.svg)

---

## 📄 Ressources utiles

* [Raylib – Documentation](https://www.raylib.com/)
* [CMake - Documentation](https://cmake.org/documentation/)

---

## 📜 Licence

Ce projet est librement utilisable à des fins pédagogiques et de formation.
