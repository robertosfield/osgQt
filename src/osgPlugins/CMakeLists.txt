#---------------------------------------------------
# OSG CMAKE SUPPORT
# (C) by Michael Wagner, mtw@shared-reality.com 2005
# (C) Eric Wing, Luigi Calori and Robert Osfield 2006-2007
#---------------------------------------------------

PROJECT(OSG_PLUGINS_MASTER)

IF(NOT DYNAMIC_OPENSCENEGRAPH)
    ADD_DEFINITIONS(-DOSG_LIBRARY_STATIC)
ENDIF()

IF(NOT MSVC)
    SET(LIBRARY_OUTPUT_PATH "${LIBRARY_OUTPUT_PATH}/${OSG_PLUGINS}")
    SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/${OSG_PLUGINS}")
ENDIF()

SET(CMAKE_SHARED_MODULE_PREFIX ${OSG_PLUGIN_PREFIX})

IF(MSVC80 OR MSVC90)
    IF(NOT OSG_MSVC_GENERATE_PLUGINS_AND_WRAPPERS_MANIFESTS)
        SET(CMAKE_MODULE_LINKER_FLAGS "${CMAKE_MODULE_LINKER_FLAGS} /MANIFEST:NO")
    ENDIF()
ENDIF()

SET(TARGET_DEFAULT_PREFIX "osgdb_")
SET(TARGET_DEFAULT_LABEL_PREFIX "Plugins")
SET(TARGET_COMMON_LIBRARIES
    OpenThreads
    osg
    osgDB
    osgUtil
)

############################################################
#
#  NodeKit/Psudo loader plugins
#

IF (QT4_FOUND)
    ADD_SUBDIRECTORY(qfont)
ENDIF()

##########to get all the variables of Cmake
#GET_CMAKE_PROPERTY(MYVARS VARIABLES)
#FOREACH(myvar ${MYVARS})
#    FILE(APPEND ${CMAKE_CURRENT_BINARY_DIR}/AllVariables.txt
#        "${myvar} -->${${myvar}}<-\n"
#    )
#ENDFOREACH(myvar)


