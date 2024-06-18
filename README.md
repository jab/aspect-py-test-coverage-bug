# Demo Aspect's py_test target with coverage

Using `bazel coverage` with a rules_python `py_test` target works:

```
❯ bazel coverage --combined_report=lcov lib_test
INFO: Using default value for --instrumentation_filter: "^//".
INFO: Override the above default with --instrumentation_filter
INFO: Analyzed target //:lib_test (114 packages loaded, 4291 targets configured).
INFO: LCOV coverage report is located at /private/var/tmp/_bazel_jab/0659ccc5740ba986ef2f2807e8233c1c/execroot/_main/bazel-out/_coverage/_coverage_report.dat
 and execpath is bazel-out/_coverage/_coverage_report.dat
INFO: From Coverage report generation:
Jun 18, 2024 11:05:55 AM com.google.devtools.coverageoutputgenerator.Main getTracefiles
INFO: Found 1 tracefiles.
Jun 18, 2024 11:05:55 AM com.google.devtools.coverageoutputgenerator.Main parseFilesSequentially
INFO: Parsing file bazel-out/darwin_arm64-fastbuild/testlogs/lib_test/coverage.dat
Jun 18, 2024 11:05:55 AM com.google.devtools.coverageoutputgenerator.Main getGcovInfoFiles
INFO: No gcov info file found.
Jun 18, 2024 11:05:55 AM com.google.devtools.coverageoutputgenerator.Main getGcovJsonInfoFiles
INFO: No gcov json file found.
Jun 18, 2024 11:05:55 AM com.google.devtools.coverageoutputgenerator.Main getProfdataFileOrNull
INFO: No .profdata file found.
INFO: Found 1 test target...
Target //:lib_test up-to-date:
  bazel-bin/lib_test
INFO: Elapsed time: 3.325s, Critical Path: 2.55s
INFO: 17 processes: 11 internal, 5 darwin-sandbox, 1 worker.
INFO: Build completed successfully, 17 total actions
//:lib_test                                                              PASSED in 1.1s
  /private/var/tmp/_bazel_jab/0659ccc5740ba986ef2f2807e8233c1c/execroot/_main/bazel-out/darwin_arm64-fastbuild/testlogs/lib_test/coverage.dat

Executed 1 out of 1 test: 1 test passes.

❯ cat /private/var/tmp/_bazel_jab/0659ccc5740ba986ef2f2807e8233c1c/execroot/_main/bazel-out/darwin_arm64-fastbuild/testlogs/lib_test/coverage.dat
SF:lib.py
FNF:0
FNH:0
DA:1,1,cIirdT1fUylQbDncHYuiLw
DA:2,1,KjVIXJCtSHJ6Jnfwt67A8Q
LH:2
LF:2
end_of_record
```

Using `bazel coverage` with an aspect-rules-py `py_test` target does not work
(note the `WARNING: There was no coverage found` in the output):

```
❯ bazel coverage --combined_report=lcov lib_test_aspect
INFO: Using default value for --instrumentation_filter: "^//".
INFO: Override the above default with --instrumentation_filter
INFO: Analyzed target //:lib_test_aspect (118 packages loaded, 4279 targets configured).
INFO: LCOV coverage report is located at /private/var/tmp/_bazel_jab/0659ccc5740ba986ef2f2807e8233c1c/execroot/_main/bazel-out/_coverage/_coverage_report.dat
 and execpath is bazel-out/_coverage/_coverage_report.dat
INFO: From Coverage report generation:
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main getTracefiles
INFO: Found 1 tracefiles.
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main parseFilesSequentially
INFO: Parsing file bazel-out/darwin_arm64-fastbuild/testlogs/lib_test_aspect/coverage.dat
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main getGcovInfoFiles
INFO: No gcov info file found.
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main getGcovJsonInfoFiles
INFO: No gcov json file found.
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main getProfdataFileOrNull
INFO: No .profdata file found.
Jun 18, 2024 11:06:40 AM com.google.devtools.coverageoutputgenerator.Main runWithArgs
WARNING: There was no coverage found.
INFO: Found 1 test target...
Target //:lib_test_aspect up-to-date:
  bazel-bin/lib_test_aspect
  bazel-bin/lib_test_aspect.venv.pth
INFO: Elapsed time: 2.495s, Critical Path: 1.31s
INFO: 18 processes: 12 internal, 5 darwin-sandbox, 1 worker.
INFO: Build completed successfully, 18 total actions
//:lib_test_aspect                                                       PASSED in 0.3s

Executed 1 out of 1 test: 1 test passes.
```
