## DeepSeek V3 Technical Report

DeepSeek is an open source LLM specializing in reasoning tasks through RL.

### Understanding LLM Inference

Decoder-*only* LLMs like GPT-3 have two phases:
1. Prefill phase (prompt processing)
	1. Compute the intermediate states for every input token
	2. Each new token depends on all previous tokens
	3. Matrix-matrix multiplication, very computation bound
2. Decode phase (token generation)
	1. Generates output tokens one at a time until stopping criteria is met
	2. Takes the last generated token and computes its query vector from Key-Value cache
	3. Matrix-vector operations, very memory-bound

### Existing Challenges

#### How can we manage a KV cache effectively?

Attention models need to store key-value vectors for each input token, a KV cache can turn Matrix-matrix multiply into matrix-vector multiply, but becomes very large as more tokens get added.

#### DeepSeek's Solution: Multi-Head Latent Attention

DeepSeek creates a compressed representation to store in the KV cache and uses a projection to bring that memory back when it is needed.

### Parallelism in Training

There are different types of parallelism:
- **Pipeline parallelism**: partition layers of the model across GPUs, so each GPU only holds a fraction of the parameters which is less memory overhead for each GPU
	- The issue with this is that some layers may be dependent on previous outputs of activation, gradients, etc.
	- To solve, you have to [[Pipeline Hazards#^3be0cf|bubble]].
- **Mixture-of-Experts (Expert) Parallelism**: only a fraction of the network is used to compute the output for any one input. Each GPU hosts "experts" of which only a subset will be activated during compute
	- The issue with this is that there is communication overhead between GPUs and gathering output from the GPUs at the end
- **DualPipe**: pipelined parallelism solution to address communication overhead, reducing bubble time. The idea is to do communication while doing computations that are unrelated (e.g. Dispatching for a *forward* task while training for a *backward* task).
	- Used in DeepSeek V3, the communication-computation-time ratio is 1:1, and under DualPipe, they claim there is near-zero communication overhead.

#### Efficient All-to-All Communication

Every GPU needs to send data to every other GPU, so they need to do GPUs → Nodes → Data Center Network. Between GPUs, this can be quick with NVIDIA NVLink (160 GB/s), but between servers it's slower with InfiniBand (50 GB/s). As a result, they used NVLink forwarding across nodes and servers.

### Routing to Experts

Since we now have experts, we can use them for specific tokens to be able to get the best results. There is a routing algorithm placed in front of the experts that dynamically choosing an expert. The problem with this is that its possible that certain experts rarely get picked so they can be left undertrained. The solution is to introduce a **bias** term that can be used to make sure that the top-$K$ model does not necessarily deterministically pull the top.

## Microsoft DeepSpeed

Meant to improve performance for Deep-learning pipelines.

### Background

Training and running Large Language Models (LLMs) runs into a few key problems: high latency, throughput scaling, model size, large overhead with many GPUs.

DeepSpeed introduces two fixes: the **DeepSpeed Transformer** and **ZeRO-Inference** (inference-time scaling technique).

### Why Fast Inferences?

Faster response times for users, higher throughput, no data dependences, lower computation cost. Scaling parameters can also be done.

### Eliminating Kernel Invocation Overhead

[[CUDA]] graph — data flows between the results of each GPU, there is a lot of overhead. We can use something called *stream capture* where you run all the kernels into a CUDA graph and then at each timestep you invoke the entire graph. This is vertical splitting of model cores.

Tensor parallelism — allows you to split the model cores horizontally across GPUs, but this means you have to combine results from multiple GPUs.