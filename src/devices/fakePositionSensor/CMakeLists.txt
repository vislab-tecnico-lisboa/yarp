# SPDX-FileCopyrightText: 2006-2021 Istituto Italiano di Tecnologia (IIT)
# SPDX-License-Identifier: BSD-3-Clause

yarp_prepare_plugin(fakePositionSensor
  CATEGORY device
  TYPE FakePositionSensor
  INCLUDE fakePositionSensor.h
  EXTRA_CONFIG
    WRAPPER=multipleanalogsensorsserver
)

if(ENABLE_fakePositionSensor)
  yarp_add_plugin(yarp_fakePositionSensor)

  target_sources(yarp_fakePositionSensor
    PRIVATE
      fakePositionSensor.cpp
      fakePositionSensor.h
  )

  target_link_libraries(yarp_fakePositionSensor
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
  )
  list(APPEND YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS
    YARP_os
    YARP_sig
    YARP_dev
  )

  yarp_install(
    TARGETS yarp_fakePositionSensor
    EXPORT YARP_${YARP_PLUGIN_MASTER}
    COMPONENT ${YARP_PLUGIN_MASTER}
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_fakePositionSensor PROPERTY FOLDER "Plugins/Device/Fake")
endif()
