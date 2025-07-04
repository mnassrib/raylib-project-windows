cmake_minimum_required(VERSION 3.10)

# Déclare le projet C
project(raylib_project C)

# Standard C99
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Dossier contenant les headers de votre projet (pas ceux de raylib)
include_directories(include)

# Fichiers source à compiler
add_executable(${PROJECT_NAME}
    src/main.c
    src/player.c
    src/utils.c
)

# === Recherche de Raylib ===

# Configuration spécifique à Windows
if(WIN32)
    # Spécifie le chemin de Raylib si installé manuellement/modifier si besoin
    set(RAYLIB_PATH "C:/raylib")
    set(CMAKE_PREFIX_PATH "${CMAKE_PREFIX_PATH};${RAYLIB_PATH}")
endif()

# Recherche de la configuration CMake de Raylib
find_package(raylib REQUIRED)

# Lie Raylib à l'exécutable
target_link_libraries(${PROJECT_NAME} raylib)

# === Lien avec bibliothèques système selon le système d'exploitation ===
if(WIN32)
    # Bibliothèques système nécessaires sous Windows
    target_link_libraries(${PROJECT_NAME}
        winmm
        gdi32
        opengl32
    )

elseif(APPLE)
    # macOS : frameworks requis uniquement si Raylib n’est pas installé via Homebrew
    find_library(COCOA_LIBRARY Cocoa)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(COREVIDEO_LIBRARY CoreVideo)
    find_library(OPENGL_LIBRARY OpenGL)

    target_link_libraries(${PROJECT_NAME}
        ${COCOA_LIBRARY}
        ${IOKIT_LIBRARY}
        ${COREVIDEO_LIBRARY}
        ${OPENGL_LIBRARY}
    )

elseif(UNIX)
    # Linux : si Raylib a été compilé manuellement
    target_link_libraries(${PROJECT_NAME}
        m
        pthread
        dl
        X11
        GL
    )
endif()
