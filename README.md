# pipelines-03682978

## How-to-reproduce
1. Create the needed resources  (`Namespace`, `Task`, `Pipeline`, `EventListener`, `TriggerBinding`, `TriggerTemplate`, `Trigger`):
   ```sh
   oc apply -k https://github.com/gmeghnag/pipelines-03682978
   ```

2. Expose the `EventListener` to create a `Route`:
   ```sh
   oc expose svc/el-test-el -n pipelines-03682978
   ```

3. Execute an `HTTP` `POST` request to trigger a new `PipelineRun`:
   ```sh
   curl -X POST -H "Content-Type: application/json" --data '{"repository": {"url": "test-url", "name": "test-reponame"}, "head_commit": {"id": "test-commit"}}' "http://$(oc get route el-test-el -n pipelines-03682978 -o jsonpath='{.spec.host}')"
   ```

