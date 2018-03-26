set(CONTROLLERS_SOURCES
    Controllers/clw_scene_controller.cpp
    Controllers/clw_scene_controller.h
    Controllers/scene_controller.h
    Controllers/scene_controller.inl)
    
set(ESTIMATORS_SOURCES 
    Estimators/estimator.h
    Estimators/path_tracing_estimator.cpp
    Estimators/path_tracing_estimator.h)

set(OUTPUT_SOURCES
    Output/clwoutput.h
    Output/output.h)
    
set(POSTEFFECT_SOURCES
    PostEffects/clw_post_effect.h
    PostEffects/post_effect.h
    PostEffects/bilateral_denoiser.h
    PostEffects/wavelet_denoiser.h)
    
set(RENDERERS_SOURCES
    Renderers/adaptive_renderer.cpp
    Renderers/adaptive_renderer.h
    Renderers/monte_carlo_renderer.cpp
    Renderers/monte_carlo_renderer.h
    Renderers/renderer.h)

set(RENDERFACTORY_SOURCES
    RenderFactory/clw_render_factory.cpp
    RenderFactory/clw_render_factory.h
    RenderFactory/render_factory.h)

set(UTILS_SOURCES
    Utils/clw_class.h
    Utils/distribution1d.cpp
    Utils/distribution1d.h
    Utils/eLut.h
    Utils/half.cpp
    Utils/half.h
    Utils/log.h
    Utils/sh.cpp
    Utils/sh.h
    Utils/shproject.cpp
    Utils/shproject.h
    Utils/sobol.h
    Utils/tiny_obj_loader.h
    Utils/toFloat.h
    Utils/version.h
    Utils/cl_inputmap_generator.cpp
    Utils/cl_inputmap_generator.h
    Utils/cl_program.cpp
    Utils/cl_program.h
    Utils/cl_program_manager.cpp
    Utils/cl_program_manager.h)

set(SCENEGRAPH_SOURCES
    SceneGraph/camera.cpp
    SceneGraph/camera.h
    SceneGraph/clwscene.h
    SceneGraph/iterator.h
    SceneGraph/light.cpp
    SceneGraph/light.h
    SceneGraph/material.cpp
    SceneGraph/material.h
    SceneGraph/scene1.cpp
    SceneGraph/scene1.h
    SceneGraph/scene_object.cpp
    SceneGraph/scene_object.h
    SceneGraph/shape.cpp
    SceneGraph/shape.h
    SceneGraph/texture.cpp
    SceneGraph/texture.h
    SceneGraph/uberv2material.cpp
    SceneGraph/uberv2material.h
    SceneGraph/inputmap.h
    SceneGraph/inputmaps.h)
    
set(SCENEGRAPH_COLLECTOR_SOURCES
    SceneGraph/Collector/collector.cpp
    SceneGraph/Collector/collector.h)
    
set(SCENEGRAPH_IO_SOURCES
    SceneGraph/IO/image_io.cpp
    SceneGraph/IO/image_io.h
    SceneGraph/IO/material_io.cpp
    SceneGraph/IO/material_io.h
    SceneGraph/IO/scene_binary_io.cpp
    SceneGraph/IO/scene_binary_io.h
    SceneGraph/IO/scene_io.cpp
    SceneGraph/IO/scene_io.h
    SceneGraph/IO/scene_test_io.cpp
    )
    
set(XML_SOURCES
    XML/tinyxml2.cpp
    XML/tinyxml2.h)

set(SOURCES
    ${CONTROLLERS_SOURCES}
    ${ESTIMATORS_SOURCES}
    ${OUTPUT_SOURCES}
    ${POSTEFFECT_SOURCES}
    ${RENDERERS_SOURCES}
    ${RENDERFACTORY_SOURCES}
    ${UTILS_SOURCES}
    ${SCENEGRAPH_SOURCES}
    ${SCENEGRAPH_COLLECTOR_SOURCES}
    ${SCENEGRAPH_IO_SOURCES}
    ${XML_SOURCES})
    
source_group("controllers" FILES ${CONTROLLERS_SOURCES})
source_group("estimators" FILES ${ESTIMATORS_SOURCES})
source_group("output" FILES ${OUTPUT_SOURCES})
source_group("posteffect" FILES ${POSTEFFECT_SOURCES})
source_group("renderers" FILES ${RENDERERS_SOURCES})
source_group("renderfactory" FILES ${RENDERFACTORY_SOURCES})
source_group("utils" FILES ${UTILS_SOURCES})
source_group("scenegraph" FILES ${SCENEGRAPH_SOURCES})
source_group("scenegraph\\collector" FILES ${SCENEGRAPH_COLLECTOR_SOURCES})
source_group("scenegraph\\io" FILES ${SCENEGRAPH_IO_SOURCES})
source_group("xml" FILES ${XML_SOURCES})

add_library(Baikal STATIC ${SOURCES})

if (BAIKAL_ENABLE_DENOISER)
    target_compile_definitions(Baikal PUBLIC ENABLE_DENOISER)
endif(BAIKAL_ENABLE_DENOISER)

if (BAIKAL_ENABLE_RAYMASK)
    target_compile_definitions(Baikal PUBLIC ENABLE_RAYMASK)
endif (BAIKAL_ENABLE_RAYMASK)

if (BAIKAL_ENABLE_UBERV2)
    target_compile_definitions(Baikal PUBLIC ENABLE_UBERV2)
endif (BAIKAL_ENABLE_UBERV2)


target_compile_features(Baikal PRIVATE cxx_std_14)
target_include_directories(Baikal PUBLIC ${Baikal_SOURCE_DIR}/Baikal)
target_link_libraries(Baikal PUBLIC RadeonRays OpenImageIO::OpenImageIO)

    