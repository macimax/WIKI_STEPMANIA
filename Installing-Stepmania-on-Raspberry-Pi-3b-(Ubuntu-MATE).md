Compiling onto a Raspberry Pi 3b was proving to be difficult with the lack of good instructions. Follow the Compiling StepMania directions until the actual compile step, then use this Shell Script.

```#!/bin/bash
git clone --depth=1 https://github.com/stepmania/stepmania.git
cd stepmania
git submodule update --init
cd Build
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release -DWITH_SSW=OFF -DWITH_CRASH_HANDLER=OFF -DWITH_MINIMAID=OFF -DWITH_SSE2=OFF .. && cmake ..
make -j2
```