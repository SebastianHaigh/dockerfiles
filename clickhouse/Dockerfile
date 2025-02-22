FROM ubuntu:latest

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

# Add LLVM repository for Clang
RUN curl -fsSL https://apt.llvm.org/llvm-snapshot.gpg.key | sudo tee /usr/share/keyrings/llvm-keyring.asc
RUN echo "deb [signed-by=/usr/share/keyrings/llvm-keyring.asc] http://apt.llvm.org/jammy/ llvm-toolchain-jammy-18 main" | sudo tee /etc/apt/sources.list.d/llvm.list

# Install Clang 19 and C++ standard library
RUN apt update && apt install -y \
    clang-19 \
    llvm-19-dev \
    libc++-19-dev \
    libc++abi-19-dev

# Set Clang 19 as default compiler
RUN update-alternatives --install /usr/bin/clang clang /usr/bin/clang-19 100 \
    && update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang-19 100

RUN apt update && apt install -y docker.io

# Set environment variables
ENV CC=clang-19
ENV CXX=clang++-19
ENV CMAKE_FLAGS="-DCMAKE_BUILD_TYPE=Debug -DENABLE_TESTS=ON -DENABLE_CLICKHOUSE_ALL=ON"

CMD ["/bin/bash"]

