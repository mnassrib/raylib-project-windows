cmake_minimum_required(VERSION 3.10)

# Utilise le nom du dossier courant comme nom de projet
get_filename_component(PROJ_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${PROJ_NAME} C)

# Utilise le standard C99
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Dossier de vos headers perso
include_directories(include)

# Fichiers sources
#file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS src/*.c) 
#add_executable(${PROJECT_NAME} ${SRC_FILES}) 
add_executable(${PROJECT_NAME} src/main.c src/player.c src/utils.c)

# === [OPTIONNEL] Ajouter un chemin personnalisé pour find_package(raylib) ===
# À activer si Raylib a été installé dans un répertoire non standard sur Windows
if(WIN32)
    # Décommentez et modifiez ce chemin si vous avez installé Raylib via CMake install
    set(RAYLIB_PATH "C:/raylib")
    set(CMAKE_PREFIX_PATH "${CMAKE_PREFIX_PATH};${RAYLIB_PATH}")
endif()

# === Tentative de détection automatique de Raylib
find_package(raylib QUIET)

if(raylib_FOUND)
    message(STATUS "Raylib trouvé via find_package()")
    target_link_libraries(${PROJECT_NAME} raylib)

else()
    message(STATUS "Raylib non trouvé via find_package() : utilisation du lien manuel")

    # Lien manuel pour Windows (Raylib copié dans MinGW)
    if(WIN32)
        target_link_libraries(${PROJECT_NAME}
            raylib
            winmm
            gdi32
            opengl32
        )
    else()
        message(SEND_ERROR "Raylib non trouvé et aucun fallback disponible (non-Windows)")
    endif()
endif()

# === Liens supplémentaires selon l'OS
if(APPLE)
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

elseif(UNIX AND NOT APPLE)
    target_link_libraries(${PROJECT_NAME}
        m
        pthread
        dl
        X11
        GL
    )
endif()
