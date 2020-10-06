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

set(SOURCES
    binding.c
    cxn.c
    library.c
    listener.c
    main.c
    session.c
    stream.c
    trace.c
    worker.c
)

add_quic_tool(quicetw ${SOURCES})

target_compile_definitions(quicetw PRIVATE _CRT_SECURE_NO_WARNINGS)

target_link_libraries(quicetw tdh)
