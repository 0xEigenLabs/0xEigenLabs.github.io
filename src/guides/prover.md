# Eigen Prover

Eigen zkVM Remote Proving Service

## Remote Proving

Remove Proving allows developers to submit their proof generation request to Eigen Proving Service.

The API is defined as below:

```
service ProverService {
  rpc ProverStream(stream ProverRequest) returns (stream ProverResponse) {}
}
```

For the ProverRequest, the request content is one of

```
message ProverRequest
{
  string id = 1;
  oneof request_type
  {
    GetStatusRequest get_status = 2;
    GenBatchProofRequest gen_batch_proof = 3;
    GenAggregatedProofRequest gen_aggregated_proof = 4;
    GenFinalProofRequest gen_final_proof = 5;
  }
}
```

The entired protobuf file can be found [here](https://github.com/0xEigenLabs/eigen-prover/blob/main/service/proto/src/proto/prover/v1/prover.proto).

The prover client example can be found in [Eigen ZETH](https://github.com/0xEigenLabs/eigen-zeth/blob/main/src/prover/provider.rs#L181).


## Local Proving Examples

The example `lr` is a very simple zkML sample, and can be proved locally fast on your desktop.

```bash
TASK=lr
export STARKJS=/zkp/eigen-zkvm/starkjs
FORCE_BIT=18 RUST_MIN_STACK=2073741821 RUST_BACKTRACE=1 RUST_LOG=debug \
    CIRCOMLIB=$STARKJS/node_modules/circomlib/circuits \
    STARK_VERIFIER_GL=$STARKJS/node_modules/pil-stark/circuits.gl \
    STARK_VERIFIER_BN128=$STARKJS/node_modules/pil-stark/circuits.bn128 \
    cargo test --release integration_test_lr -- --nocapture
```
Note that the `FORCE_BIT` can be adjusted as per to different circuits.
Taking Fibonacci as an example, the recursive proof process is shown in the figure below.

If you intend to enable the avx acceleration:

```
# for avx512
RUSTFLAGS='-C target-cpu=native' FORCE_BIT=18 RUST_MIN_STACK=2073741821 RUST_BACKTRACE=1 RUST_LOG=debug \
    CIRCOMLIB=$STARKJS/node_modules/circomlib/circuits \
    STARK_VERIFIER_GL=$STARKJS/node_modules/pil-stark/circuits.gl \
    STARK_VERIFIER_BN128=$STARKJS/node_modules/pil-stark/circuits.bn128 \
    cargo test --release integration_test --features avx512

# for avx2 only (without avx512)
RUSTFLAGS='-C target-cpu=native' FORCE_BIT=18 RUST_MIN_STACK=2073741821 RUST_BACKTRACE=1 RUST_LOG=debug \
    CIRCOMLIB=$STARKJS/node_modules/circomlib/circuits \
    STARK_VERIFIER_GL=$STARKJS/node_modules/pil-stark/circuits.gl \
    STARK_VERIFIER_BN128=$STARKJS/node_modules/pil-stark/circuits.bn128 \
    cargo test --release integration_test
```

## Proving Architecture
<center>
<img src="/img/zkvm/proving-architecture.png">
</center>


## Request Lifecycle

<center>
<img src="/img/zkvm/eigen-prover/prover-dataflow.png">
</center>

## Deployment

[Document](https://github.com/0xEigenLabs/eigen-prover?tab=readme-ov-file#server)
