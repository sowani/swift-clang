include(CheckIncludeFiles)

set(LLVM_LINK_COMPONENTS support)

add_clang_library(clangDirectoryWatcher
  DirectoryWatcher.cpp

  LINK_LIBS
  clangBasic
  )

if(BUILD_SHARED_LIBS)
  if(APPLE)
    check_include_files("CoreServices/CoreServices.h" HAVE_CORESERVICES_H)
    if(HAVE_CORESERVICES_H)
      set(DIRECTORY_WATCHER_FLAGS "${DIRECTORY_WATCHER_FLAGS} -framework CoreServices")
    endif()
    set_property(TARGET clangDirectoryWatcher APPEND_STRING PROPERTY
                 LINK_FLAGS ${DIRECTORY_WATCHER_FLAGS})
  endif()
endif()
