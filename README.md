# Code coverage

## Unit tests

#### **go test**
`go test -v -coverprofile test-reports/unit.out -covermode=count ./pkg/...`
Enable coverage analysis in *count* mode. Write a coverage profile to *test-reports/unit.out* after all tests have passed.

## Integration tests

### **Standalone server**
1. Create binary
`go test -c -covermode=count -coverpkg ./... ./cmd/server`
2. Start server
`./server.test -test.coverprofile=it.out`
3. Run integration tests

4. Stop server
` Ctrl+C`

Compile the test binary to *server.test* but do not run it. Enable coverage analysis in *count* mode. Write a coverage profile to *test-reports/it.out* after all tests have passed.

OR

#### **Docker container**
1. Create image

2. Run tests


Create a docker image with test binary. Enable coverage analysis in *count* mode. Write a coverage profile to */etc/it.out* (inside container) after all tests have passed. Copy */etc/it.out* to *test-reports/it.out* on host.

## Merge coverage profiles
1. Install **_gocovmerge_**.
`go get github.com/wadey/gocovmerge`
2. Merge the coverage profiles.
`gocovmerge test-reports/unit.out test-reports/it.out > test-reports/total.out`

## Visualize code coverage

#### Display coverage percentages to stdout for each function:
`go tool cover -func=test-reports/total.out`
The last line in output is total coverage.

#### Open a web browser displaying annotated source code:
`go tool cover -html=test-reports/total.out`
***
