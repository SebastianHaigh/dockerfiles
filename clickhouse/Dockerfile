FROM ubuntu:22.04

# Install basic dependencies
RUN apt update && apt install -y \
    sudo cmake ninja-build \
    ccache nasm yasm\
    lld gdb valgrind \
    git pkg-config \
    python3 python3-pip \
    libssl-dev \
    vim less tmux \
    curl wget unzip zstd

# Add LLVM repository for Clang 18
RUN curl -fsSL https://apt.llvm.org/llvm-snapshot.gpg.key | sudo tee /usr/share/keyrings/llvm-keyring.asc
RUN echo "deb [signed-by=/usr/share/keyrings/llvm-keyring.asc] http://apt.llvm.org/jammy/ llvm-toolchain-jammy-18 main" | sudo tee /etc/apt/sources.list.d/llvm.list

# Install Clang 18 and C++ standard library
RUN apt update && apt install -y \
    clang-18 \
    llvm-18-dev \
    libc++-18-dev \
    libc++abi-18-dev

# Set Clang 18 as default compiler
RUN update-alternatives --install /usr/bin/clang clang /usr/bin/clang-18 100 \
    && update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang-18 100

# Set environment variables
ENV CC=clang-18
ENV CXX=clang++-18
ENV CMAKE_FLAGS="-DCMAKE_BUILD_TYPE=Debug -DENABLE_TESTS=ON -DENABLE_CLICKHOUSE_ALL=ON"

CMD ["/bin/bash"]

