## EigenCC Privacy Operators
It's easy to develop new privacy operators via EigenCC Framework.

### Steps
1. Define the service.
A service could be a collection of methods handling the private object on Blockchain.
A built-on Echo service [here](https://github.com/0xEigenLabs/eigencc/blob/main/sgx/services/fns/sgx_trusted_lib/src/trusted_worker/demo_func.rs#L25) is provided:

```
pub struct EchoWorker {
    worker_id: u32,
    func_name: String,
    input: Option<EchoWorkerInput>,
}
```

* `worker_id` must be unique globally, an integer beginning at 0, increased by service.
* `func_name` is the service name, and also the second argument of [eigen_create_task](https://github.com/0xEigenLabs/eigencc/blob/main/sgx/sdk/c_sdk/include/eigen/eigentee.h#L70)
* `input` : arguments of service;

2. Define the service input
An input is a structure containing the arguments of each service call. the [EchoWorkerInput](https://github.com/0xEigenLabs/eigencc/blob/main/sgx/services/fns/sgx_trusted_lib/src/trusted_worker/demo_func.rs#L40)
recepts a `String` value. Usually, we need preprocessing for the input before being fed into service execution.

3. Define service side logic
All the handling logic should be defined in the `execute` function:
```
fn execute(&mut self, _context: WorkerContext) -> Result<String>
```

4. Register the service

Expose the service to EigenCC framework by adding
```
mod service_source_file_name;
pub use service_source_file_name::service_struct_name;
```
to [mod.rs](https://github.com/0xEigenLabs/eigencc/blob/main/sgx/services/fns/sgx_trusted_lib/src/trusted_worker/mod.rs)

1. Define client side logic

Call the  service by c or rust [SDK](https://github.com/0xEigenLabs/eigencc/blob/main/sgx/sdk/c_sdk/include/eigen/eigentee.h).
