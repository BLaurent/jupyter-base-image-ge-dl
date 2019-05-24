cmake_minimum_required(VERSION 3.4)

set(API_PROXY ${CMAKE_CURRENT_SOURCE_DIR})
SET(IMAGE_TAG "registry.gear.ge.com/foundry-eu/jupyter-base-image-ge-dl")
SET(build-args --build-arg 'http_proxy=$ENV{http_proxy}' --build-arg 'https_proxy=$ENV{https_proxy}' --build-arg 'no_proxy=$ENV{no_proxy}' --build-arg 'ARTIFACTORY_CREDS_USR=$ENV{ARTIFACTORY_CREDS_USR}' --build-arg 'ARTIFACTORY_CREDS_PSW=$ENV{ARTIFACTORY_CREDS_PSW}' --build-arg ARTIFACTORY_REPOSITORY="IEWMS-SNAPSHOT" )

add_custom_target(build
  COMMAND docker build ${build-args} --tag=${IMAGE_TAG} .
  WORKING_DIRECTORY ${IMAGE_PATH})


add_custom_target(build-noproxy
  COMMAND docker build --tag=${IMAGE_TAG} .
  WORKING_DIRECTORY ${IMAGE_PATH})
