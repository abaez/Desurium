include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/code
  ${SERVICECORE_INCLUDE_DIRS}
)

set(IPC_PIPE_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/code PARENT_SCOPE)

file(GLOB Sources code/IPCClass.cpp
                  code/IPCManager.cpp
                  code/IPCParameter.cpp
)

if(WIN32)
  file(GLOB PlattformSources code/IPCPipeBase.cpp
                             code/IPCPipeClient.cpp
                             code/IPCPipeServer.cpp
)
else()
  file(GLOB PlattformSources code/IPCPipeBase_Nix.cpp
                             code/IPCPipeClient_Nix.cpp
                             code/IPCPipeServer_Nix.cpp
)
endif()

add_library(ipc_pipe STATIC ${Sources} ${PlattformSources})

target_link_libraries(ipc_pipe
    threads
    util
    ${TINYXML_LIBRARIES}
)
