# Copyright (c) Microsoft Corporation.
# Licensed under the MIT License.

function(add_quic_tool)
    set(targetname ${ARGV0})
    list(REMOVE_AT ARGV 0)

    add_executable(${targetname} ${ARGV})
    target_link_libraries(${targetname} inc warnings msquic platform inc)
    set_property(TARGET ${targetname} PROPERTY FOLDER "tools")
endfunction()

function(quic_tool_warnings)
    target_link_libraries(${ARGV0} warnings)
endfunction()

set(SOURCES QuicEventCollection.cpp)

add_library(msquicetw STATIC ${SOURCES})

target_link_libraries(msquicetw PRIVATE inc)

set_property(TARGET msquicetw PROPERTY FOLDER "tools")
