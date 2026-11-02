# Schwarzschild Ray Tracer

Renders a black hole by integrating null geodesics per ray in C++17, multithreaded with OpenMP.

![Sample output](assets/sample_output.jpg)

Each pixel's ray is integrated through the Schwarzschild metric. Rays that escape take their color from a spherical background image (`assets/background.jpg`).

## Build and run

Needs CMake 3.12+, a C++17 compiler and OpenMP. GoogleTest is fetched by CMake.

```sh
cmake -B build -S . -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release
```

Run from the repository root, since it reads `assets/background.jpg` by a relative path:

```sh
./build/SchwarzschildSim                 # Linux / macOS
.\build\Release\SchwarzschildSim.exe      # Windows / MSVC
```

It writes the render to `output.jpg`.

## Tests

GoogleTest unit tests for the vector math and relativity modules:

```sh
ctest --test-dir build -C Release
```

## Layout

```
math/core/          tensor.hpp, vec4.hpp
math/relativity/    relativity.hpp (metric), geodesic.hpp
renderer/           camera.hpp (ray setup, OpenMP render loop)
tests/              test_vec4.cpp, test_relativity.cpp
libs/stb/           image loading and writing
assets/             background and sample output
```

## Credits

The math and overall approach follow James' tutorial, ["Implementing General Relativity: Rendering the Schwarzschild black hole, in C++"](https://20k.github.io/c++/2024/05/31/schwarzschild.html) (May 31, 2024). The code here is my own implementation. Image I/O uses [stb](https://github.com/nothings/stb).

## License

MIT. See [LICENSE](LICENSE).
