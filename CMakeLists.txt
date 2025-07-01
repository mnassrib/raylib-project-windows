cmake_minimum_required(VERSION 3.10)

# Déclare le projet C en spécifiant le nom
project(raylib_project C)

# Spécifie le standard C
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Inclut les headers du projet
include_directories(include)

# Ajoute les fichiers source
add_executable(${PROJECT_NAME}
    src/main.c
    src/player.c
    src/utils.c
)

# --- Trouver Raylib et lier selon l'OS ---
if(WIN32)
    # Configuration spécifique à Windows
    set(CMAKE_PREFIX_PATH "C:/raylib")  # Adapté à votre installation
    find_package(raylib REQUIRED)
    target_link_libraries(${PROJECT_NAME} raylib winmm) 
    
elseif(APPLE)
    # macOS (Raylib doit être installé via Homebrew)
    find_package(raylib REQUIRED)
    target_link_libraries(${PROJECT_NAME} raylib)
    
elseif(UNIX)
    # Linux ou WSL
    find_package(raylib REQUIRED)
    target_link_libraries(${PROJECT_NAME} raylib m)  
endif()