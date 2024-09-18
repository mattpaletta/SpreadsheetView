file(GLOB_RECURSE CMAKE_FILES *.txt)
file(GLOB_RECURSE SRC_FILES Sources/*.swift)

add_library(SpreadsheetView SHARED ${SRC_FILES})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${SRC_FILES} ${CMAKE_FILES})
target_include_directories(SpreadsheetView PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(SpreadsheetView PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(SpreadsheetView PUBLIC "-framework UIKit")

set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_DEFINES_MODULE "YES")
set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_PRODUCT_MODULE_NAME "SpreadsheetView")
set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_PRODUCT_BUNDLE_IDENTIFIER "com.paletta.SpreadsheetView")
set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_CLANG_ENABLE_MODULES "YES")
set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_CLANG_ENABLE_OBJC_ARC "YES")

set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_RUN_CLANG_STATIC_ANALYZER "NO")

set_target_properties(SpreadsheetView PROPERTIES XCODE_ATTRIBUTE_SWIFT_VERSION "5")
set_target_properties(SpreadsheetView PROPERTIES
   FRAMEWORK TRUE
   FRAMEWORK_VERSION A
   MACOSX_FRAMEWORK_IDENTIFIER com.paletta.SpreadsheetView
   #MACOSX_FRAMEWORK_INFO_PLIST Sources/Info.plist
   PUBLIC_HEADER ${CMAKE_CURRENT_SOURCE_DIR}/Sources/SpreadsheetView.h
   XCODE_ATTRIBUTE_CODE_SIGN_IDENTITY "iPhone Developer"
   #XCODE_ATTRIBUTE_SWIFT_OBJC_BRIDGING_HEADER "${CMAKE_CURRENT_SOURCE_DIR}/SpreadsheetView-Bridging.h"
)

file(GLOB TEST_SRC_FILES Tests/*.swift Tests/*.mm)
cpptest_configure_target(
    TARGET SpreadsheetView
    TEST_SRC_FILES ${TEST_SRC_FILES}
)
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${TEST_SRC_FILES})
