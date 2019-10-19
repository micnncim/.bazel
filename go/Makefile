.PHONY: dep
dep: bin/bazelisk
	go mod tidy
	bin/bazelisk run //:gazelle
	bin/bazelisk run //:gazelle -- update-repos -from_file=go.mod -to_macro=build/bazel/deps.bzl%go_repositories

.PHONY: run
run: bin/bazelisk
	bin/bazelisk run //cmd/<<PROJECT>>

.PHONY: build
build: bin/bazelisk
	bin/bazelisk build //...

.PHONY: test
test: bin/bazelisk
	bin/bazelisk test //...

.PHONY: buildifier
buildifier: bin/bazelisk
	bin/bazelisk run //:buildifier

.PHONY: clean
clean: bin/bazelisk
	bin/bazelisk clean

.PHONY: coverage
coverage:
	go test -v -race -covermode=atomic -coverpkg=./... -coverprofile=coverage.txt ./...

.PHONY: expose-generated-go
 expose-generated-go:
	./hack/expose-generated-go.sh <<OWNER>> <<PROJECT>>

bin/bazelisk:
	@mkdir -p bin
	go build -o bin/bazelisk github.com/bazelbuild/bazelisk
