cmake_minimum_required(VERSION 3.8)
project("amswarm")

# 设置 C++17 标准并启用其他标志
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fthreadsafe-statics -fvisibility-inlines-hidden")

# 确保在调试版本中生成了完整的调试信息
# set(CMAKE_CXX_FLAGS_DEBUG "-O0 -g")
# set(CMAKE_BUILD_TYPE Debug)

# 依赖包
find_package(OpenMP)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
find_package(eigen-quadprog)
find_package(nlohmann_json)

# 添加include路径
include_directories(include/)

# 添加am算法的单独测试路径
set(TEST_AM_SRC ${PROJECT_SOURCE_DIR}/main.cpp
    ${PROJECT_SOURCE_DIR}/src/optim_am_swarm.cpp
    ${PROJECT_SOURCE_DIR}/src/sim_am_swarm.cpp
)
add_executable(gen_traj ${TEST_AM_SRC})
target_link_libraries(gen_traj eigen-quadprog nlohmann_json -lpthread -lglog)