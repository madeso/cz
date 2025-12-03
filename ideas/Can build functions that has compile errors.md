## Can build functions that has compile errors

They will assert/crash at runtime with an error but this might be desirable if you know during a refactor that some part of the code is never touched but you want to test the assumption that the refactor fixed a bug/improved perf.